# How to Deploy a React App to AWS S3

1.- You need to have a AWS account. You can follow the next link:

	https://aws.amazon.com/
	
##### NOTE: If you already have it, skip this step.

2.- After Logged-in choose the service called "S3" and press the button that it says "CREATE A BUCKET".

3.- Now, you have to fill out the form:

- Write a Bucket Name (i.e. reactjs123)
- Choose a region
- Press button "CREATE"

4.- As the bucket is already created, press it to go into the settings.

5.- Choose the tab called ***"PERMISSIONS"*** and press ***"BLOCK PUBLIC ACCESS"***, after choose ***"EDIT"***, then unchecked the option says ***"BLOCK ALL PUBLIC ACCESS"*** and finally press ***"SAVE"***.

6.- At the same tab ***"PERMISSIONS"***, we have to choose the option ***"BUCKET POLICY"*** and paste the next configuration object and after press ***"SAVE"***.
```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::reactjs123/*"
        }
    ]
}
```
##### NOTE: Remember that the bucket is called "reactjs123", otherwise you have to replace with your bucket name at the policy object.
\
7.- Now we have to build our react app before to upload it. At the console we run the next command:
```sh
npm run build
```
8.- As we already have builded our React-App, now we need to upload it. we have two options, by the ***"web interface"*** our by command line using ***"aws cli"***.

8.1.- WEB INTERFACE
At the tab called "OVERVIEW" press the button Upload, then you have to choose the files are into the "build" directory.(That directory it was created at the step number 7)
    
8.2.- AWS CLI 

***Requirement: to have installed aws cli.***

You have to be into the project directory (i.e. reactjs123/) and run the next command.

     $ aws s3 sync build/ s3://reactjs123
    
    
###### NOTE: To install aws cli check this link https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html

9.- at the last step you have to go to the tab called ***"PROPERTIES"*** and press at the option ***"STATIC WEBSITE HOSTING"***, and do the next:

    - Choose the option "Use this bucket to host a website"
    - at the "Index document" field write "index.html"
    - at the "Error document" field write "index.html"
    - and finally press "SAVE"

Now you already can see your react-app.

##### NOTE: you can find the Endpoint at the top of the tab "STATIC WEBSITE HOTING", it's going to looks like this "http://reactjs123.s3-website-us-west-2.amazonaws.com"


 

