# RAPS

Risk After Prostate Surgery Shiny [Web Application](http://predict.shinyapps.io/raps)

We have developed a tool called RAPS (Risks After Prostate Surgery) that uses a man’s personal characteristics to estimate his probability of: a) prostate cancer recurrence, and b) dying without 
recurrence within 10 years of radical prostatectomy for his cancer.

# Deployment Instructions

#### Clone the repo
You must clone the code base to work on it.

      git clone https://github.com/vsoch/prostate

or if you use ssh for github

      git clone git@github.com:vsoch/prostate.git
   
Note that the app is named on the server according to the folder name. The folder is called "prostate," so this would be deployed as `http://predict.shinyapps.io/prostate`. To fix this, and deploy as "raps," change the folder name:

      mv prostate raps 

Do not CD into the folder, you will work one level above it to deploy. It is most comfortable to work in the [rstudio](https://www.rstudio.com/) environment. If you have not installed it, do so, and run as so from the command line:

      rstudio

Once in R, you need to install devtools, shiny, and shiny apps.

      install.packages('devtools')
      install.packages('shiny')

      if (!require("devtools"))
        install.packages("devtools")
        devtools::install_github("rstudio/shinyapps")

If any installations don't work, it is recommended to find the source code on github, and install from source instead of a repository.

#### Setting up R
First, load the shinyapps, shiny, and devtools

      library('devtools')
      library('shiny')
      library('shinyapps')

You must first log into [shinyapps.io](http://shinyapps.io) to get the token and secret to use in R. Click on `Account` then `Tokens` and then `Show`. You will need to click `show secret` and `copy to clipboard` to copy the entire line of code and then copy paste into rstudio. Do that.

Make sure you are one folder above the app, you can check by doing "list.files()" and you should see "raps." When you are, the command to deploy is:
     
     deployApp("raps",account="predict")

The browser will open when it is finished.

#### Notes about the application
Shiny applications are usually required to have a `server.R` and `ui.R`. More advanced apps can roll their own html, meaning that we get rid of the `ui.R` and replace with an [index.html](www/index.html) file in the `www` folder. Note that it MUST be called this, and is expecting it. Thus, to make changes to the UI, you must change this file. Changes to the computation or the "R part" of the server should be changed in [server.R](server.R).
