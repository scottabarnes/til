# Extracting rules from a decision tree

I wanted to get the rules from a decision tree in an easy to read format for interpretation.  I came across this great [blog post](https://mljar.com/blog/extract-rules-decision-tree/) which provided code to get the rules from a decision tree in a number of formats.

The Scikit-learn decision tree class has an export_text() method which returns the text representation of the rules.



    from matplotlib import pyplot as plt
    from sklearn import datasets
    from sklearn.tree import DecisionTreeClassifier 
    from sklearn import tree

    # Prepare the data data
    iris = datasets.load_iris()
    X = iris.data
    y = iris.target

    # Fit the classifier with max_depth=3
    clf = DecisionTreeClassifier(max_depth=3, random_state=42)
    model = clf.fit(X, y)

    text_representation = tree.export_text(clf, feature_names=iris.feature_names)
    print(text_representation)

The blog post also has some code for obtaining the rules in human readable format. It makes use of [`_tree`](https://github.com/scikit-learn/scikit-learn/blob/10a5468e90797e0e5ec249e35f457c3404d69f98/sklearn/tree/_tree.pxd) in `sklearn.tree`. Snippet below -  credit for the code to Piotr Płoński, the author of the blog post.  

    def get_rules(tree, feature_names, class_names):
        tree_ = tree.tree_
        feature_name = [
            feature_names[i] if i != _tree.TREE_UNDEFINED else "undefined!"
            for i in tree_.feature
        ]

        paths = []
        path = []
        
        def recurse(node, path, paths):
            
            if tree_.feature[node] != _tree.TREE_UNDEFINED:
                name = feature_name[node]
                threshold = tree_.threshold[node]
                p1, p2 = list(path), list(path)
                p1 += [f"({name} <= {np.round(threshold, 3)})"]
                recurse(tree_.children_left[node], p1, paths)
                p2 += [f"({name} > {np.round(threshold, 3)})"]
                recurse(tree_.children_right[node], p2, paths)
            else:
                path += [(tree_.value[node], tree_.n_node_samples[node])]
                paths += [path]
                
        recurse(0, path, paths)

        # sort by samples count
        samples_count = [p[-1][1] for p in paths]
        ii = list(np.argsort(samples_count))
        paths = [paths[i] for i in reversed(ii)]
        
        rules = []
        for path in paths:
            rule = "if "
            
            for p in path[:-1]:
                if rule != "if ":
                    rule += " and "
                rule += str(p)
            rule += " then "
            if class_names is None:
                rule += "response: "+str(np.round(path[-1][0][0][0],3))
            else:
                classes = path[-1][0][0]
                l = np.argmax(classes)
                rule += f"class: {class_names[l]} (proba: {np.round(100.0*classes[l]/np.sum(classes),2)}%)"
            rule += f" | based on {path[-1][1]:,} samples"
            rules += [rule]
            
        return rules

        rules = get_rules(clf, iris.feature_names, iris.target_names)
        for r in rules:
            print(r)    