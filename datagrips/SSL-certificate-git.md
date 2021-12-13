# SSL certificate error when pushing to git

Had just installed datagrips and was trying to get git integration set up. Was seeing an error:

    
    SSL certificate problem: unable to get local issuer certificate

Found that reinstalling git and selecting the option to use the native windows secure channel library as suggested in this stackoverflow [post](https://stackoverflow.com/a/45695638) resolved this. 