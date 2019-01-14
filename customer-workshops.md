# DeepLens-workshops

In this workshop you will learn how to build a sentiment analysis project for your DeepLens. This project was submitted by Ricardo Mota and Jidesh Veeramachaneni as part of the DeepLens Hackathon challenge.

In this project you will learn to build a deep learning model to identify and analyze the sentiments of your audience

## In this workshop you will learn the following:

1. How to build and train a face detection model in SageMaker
2. Modify the DeepLens inference Lambda function to upload cropped faces to S3
3. Deploy the inference Lambda function and face detection model to DeepLens
4. Create a Lambda function to trigger Rekognition to identify emotions
5. Create a DynamoDB table to store the recognized emotions
6. Analyze using CloudWatch

![image](https://user-images.githubusercontent.com/11222214/37996605-1ba4be34-31cd-11e8-9e25-ba3a1cdbc9db.png)

The workshop consists of 4 hands-on lab sessions:

# Hands-on Lab 1: Build and train a face detection model in SageMaker

In this lab, you will build and train a face detection model. You can find the instructions here: [SageMaker lab](https://github.com/fibbonnaci/DeepLens-workshops/tree/master/SageMaker%20lab)

# Hands-on Lab 2: Register and configure your DeepLens device

## Register AWS DeepLens

Visit [AWS Management Console](https://console.aws.amazon.com/console/home?region=us-east-1). Make sure you are on *US-East (N.Virginia) region*.

Search for DeepLens in the search bar and select AWS DeepLens to open the console.

The instructions for this hands-on lab is here: [Registration and deployment](https://github.com/fibbonnaci/DeepLens-workshops/blob/master/Registration%20and%20project%20deployment/readme.md)

On the AWS DeepLens console screen, find the Get started section on the right hand side and select Register Device.

![register device landing page](https://user-images.githubusercontent.com/11222214/38656972-a73f8bd4-3dd2-11e8-8275-0486f8d78d2d.JPG)

### Step 1- Provide a name for your device.

Enter a name for your DeepLens device (for example, “MyDevice”), and select Next.

![name device](https://user-images.githubusercontent.com/11222214/38656982-b8d2b3d0-3dd2-11e8-9d00-060ccf015d0c.JPG)

### Step 2- Provide permissions

AWS DeepLens projects require different levels of permissions, which are set by AWS Identity and Access Management (IAM) roles. When registering your device for the first time, choose **Create roles** under Permissions to have the required IAM roles created. 

![create roles](https://user-images.githubusercontent.com/11222214/41578790-cad777a4-7348-11e8-97b1-b12f9a8f6549.jpg)

Then choose **Next**

![create roles- next](https://user-images.githubusercontent.com/11222214/41578802-e0c3ccc0-7348-11e8-9690-27adb740049c.jpg)

### Step 3- Download certificate
In this step, you will download and save the required certificate to your computer. You will use it later to enable your DeepLens to connect to AWS.

Select Download certificate and note the location of the certificates.zip file. Note: Do not open the zip file. You will attach this zip file later on during device registration.

![download certificate](https://user-images.githubusercontent.com/11222214/41578863-2fe8e4e8-7349-11e8-999b-8b4890bd4136.JPG)

Select **Continue.**

![download certificate- continue](https://user-images.githubusercontent.com/11222214/41578893-5b928842-7349-11e8-867b-bf79d293bd2f.JPG)


## Configure your DeepLens

In this step, you will connect the device to a Wi-Fi/Ethernet connection, upload the certificate and review your set-up. Then you're all set!

Power ON your device

<details> <summary>If you are connected over monitor setup </summary>
  
  Make sure the middle LED is blinking. If it is not, then use a pin to reset the device. The reset button is located at the back of the device
  
 Navigate to the setup page by choosing **Complete the setup** 
 
 ![last step](https://user-images.githubusercontent.com/11222214/41578985-c854efba-7349-11e8-8c73-62267c61091a.JPG)
  
</details>
  
<details> <summary>If you are connected in headless mode </summary>
  
  Make sure the middle LED is blinking. If it is not, then use a pin to reset the device. The reset button is located at the back of the device
  
  Locate the SSID/password of the device’s Wi-Fi. You can find the SSID/password on the underside of the device.
  
  Connect to the device network via the SSID and provide the password
  
  Navigate to the setup page by choosing **Complete the setup** 
  
  ![last step](https://user-images.githubusercontent.com/11222214/41578985-c854efba-7349-11e8-8c73-62267c61091a.JPG)
  
</details>

### Step 4- Connect to your network

Select your local Wi-Fi network ID from the dropdown list and enter your WiFi password. If you are using Ethernet, choose Use Ethernet option instead.

Select Save.

![network connection](https://user-images.githubusercontent.com/11222214/38657139-77c96aa4-3dd3-11e8-8cba-97dc3c47fc66.JPG)

If this is your first time registering the device, you will see the updates available screen. Choose **Install and Reboot** It will take couple of minutes for the updates to come through. After the updates are installed, the device will reboot automatically

![install and reboot](https://user-images.githubusercontent.com/11222214/41579269-14d84e30-734b-11e8-8894-c4a76f1715d5.JPG)

On rebooting, the device will come back to the install and reboot screen. From the URL, delete the `#softwareUpdate`

![software update remove](https://user-images.githubusercontent.com/11222214/41579379-a3deed32-734b-11e8-894a-c209cb7a7cca.JPG)

### Step 5- Attach Certificates

Select Browse in the Certificate section. Select the zip file you downloaded in Step 4 

Select Next.

![upload certificate](https://user-images.githubusercontent.com/11222214/38657156-8cc8c5b2-3dd3-11e8-9261-dda8a8925cca.JPG)

### Step 6- Download Streaming Certificate

Choose **Download** . Then choose **Next**

![download streaming cert](https://user-images.githubusercontent.com/11222214/41579452-e253dca8-734b-11e8-9a47-5a7f48b6a0db.JPG)

### Step 7- Device set up.

If you are on the device summary page: please do not make changes to the password.

Note: Instead, if you are presented with the below screen, type the device password as `Aws2017!`. 

![device settings](https://user-images.githubusercontent.com/11222214/38657201-c44385fe-3dd3-11e8-8497-7add710be21b.JPG)

### Step 7- Select Finish

![summary](https://user-images.githubusercontent.com/11222214/41579495-0d5235e4-734c-11e8-987a-18a0b83259cc.JPG)


Congratulations! You have successfully registered and configured your DeepLens device. To verify, return to [AWS DeepLens console](https://console.aws.amazon.com/deeplens/home?region=us-east-1#projects) and select **Devices** in the left side navigation bar and verify that your device has completed the registration process. You should see a green check mark and Registered under Registration status.

![device registered successfully](https://user-images.githubusercontent.com/11222214/41579540-3cc3560a-734c-11e8-82c0-6fc18c3952c8.JPG)


# Hands-on Lab 3: Build a project to detect faces and send the cropped faces to S3 bucket

#### IAM Roles:

First, we need to add S3 permissions to the DeepLens Lambda role so the Lambda function on the device can call `PutObject` on the bucket of interest.

Go to [IAM Console](https://console.aws.amazon.com/iam/home?region=us-east-1#/home)

Choose Roles and look up `AWSDeepLensGreenGrassGroupRole`

Click on the role, and click Attach Policy

Search for `AmazonS3FullAccess` and choose the policy by checking the box and click on Attach Policy

#### Create Bucket:

We need to create an S3 bucket that we can upload faces to.

- Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for S3
- Choose 'Create bucket'
- Name your bucket: `face-detection-`_your-name_
- Click on Create 

#### Create Inference Lambda function:

- Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Lambda
- Click **Create function**
- Choose **Blueprints**
- In the search bar, type “greengrass-hello-world” and hit Enter
- Choose the python blueprint and click Configure
- Name the function: `DeepLens-sentiment-`_your-name_
- Role: Choose an existing role
- Existing Role: `AWSDeepLensLambdaRole`
- Click **Create Function**

Replace the default script with the [inference script](https://github.com/fibbonnaci/DeepLens-workshops/blob/master/Inference%20Lambda/inference-lambda.py) . You can select the inference script, by selecting Raw in the Github page and choosing the script using Ctrl+A/Cmd+A . Copy the script and paste it into the Lambda function (make sure you delete the default code).

In the script, you will have to provide the name for your S3 bucket. Insert your bucket name in the code below:

![code bucket](https://user-images.githubusercontent.com/11222214/38719807-b46169fa-3ea8-11e8-8ff2-69af5455ede7.jpg)

Click Save.

Under the “Actions” drop-down menu, Click **Publish new version** and publish.

Note: It is important that you publish the Lambda function or else you cannot access it from the DeepLens console.

#### Deploy project:

**Step 1- Create Project**

The AWS DeepLens console should open on the Projects screen, select **Create new project** on the top right (if you don’t see the project list view, click on the hamburger menu on the left and select Projects)

![create project](https://user-images.githubusercontent.com/11222214/38657905-82207e44-3dd7-11e8-83ef-52049e229e33.JPG)

- Choose a blank template and scroll down the screen to select Next
- Provide a name for your project: `face-detection-`_your-name_
- Click on **Add Models** and choose face detection
- Click on **Add function** and choose the Lambda function you just created
- Click **Create**

**Step 2- Deploy to device**
In this step, you will deploy the Face detection project to your AWS DeepLens device.

- Select the project you just created from the list by choosing the radio button
- Select **Deploy to device**

![choose project-edited-just picture](https://user-images.githubusercontent.com/11222214/38657988-eb9d98b6-3dd7-11e8-8c94-7273fcfa6e1b.jpg)

On the Target device screen, choose your device from the list, and select **Review**

![target device](https://user-images.githubusercontent.com/11222214/38658011-088f81d2-3dd8-11e8-972a-9342b7b3e291.JPG)

Select Deploy.

![review deploy](https://user-images.githubusercontent.com/11222214/38658032-223db2e8-3dd8-11e8-9bdf-04779cd0e0e6.JPG)

On the AWS DeepLens console, you can track the progress of the deployment. It can take a few minutes to transfer a large model file to the device. Once the project is downloaded, you will see a success message displayed and the banner color will change from blue to green.

**Confirmation/verification**

You will find your cropped faces uploaded to your S3 bucket.


# Hands-on Lab 4: Identify emotions

**Step 1- Create DynamoDB table**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Dynamo

- Click on **Create Table**
- Name of the table: `recognize-emotions-`_your-name_
- Primary key: `s3key`
- Click on **Create**. This will create a table in your DynamoDB.

**Step 2- Create a role for cloud lambda function**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for IAM

- Choose **Create Role**
- Select **AWS Service**
- Select **Lambda** and choose **Next: Permissions**

Attach the following policies: 

* ``AmazonDynamoDBFullAcces``
* ``AmazonS3FullAccess``
* ``AmazonRekognitionFullAccess``
* ``CloudWatchFullAccess``

Click **Next**

- Provide a name for the role: ``rekognizeEmotions``
- Choose **Create role**


**Step 3- Create a Lambda function that runs in the cloud**

The inference Lambda function that you deployed earlier will upload the cropped faces to your S3 bucket. On S3 upload, this new Lambda function gets triggered and runs the Rekognize Emotions API by integrating with Amazon Rekognition. 

- Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Lambda
- Click **Create function**
- Choose **Author from scratch**
- Name the function: `recognize-emotion-`_your-name_
- Runtime: Choose Python 2.7
- Role: Choose an existing role
- Existing role: `rekognizeEmotions`
- Choose **Create function**

Replace the default script with the script in [recognize-emotions.py](https://github.com/fibbonnaci/DeepLens-workshops/blob/master/Integrate%20with%20Rekognition/rekognize-emotions.py). You can select the script by selecting Raw in the Github page and choosing the script using Ctrl+A/Cmd+A. Copy the script and paste it into the Lambda function (make sure you delete the default code).

Make sure you enter the table name you created earlier in the section highlighted below:

![dynamodb](https://user-images.githubusercontent.com/11222214/38838790-b8b72116-418c-11e8-9a77-9444fc03bba6.JPG)


Next, we need to add the event that triggers this Lambda function. This will be an “S3:ObjectCreated” event that happens every time a face is uploaded to the face S3 bucket. Add an S3 trigger from the left side of the Designer section in the Lambda console.

Configure with the following:

- Bucket name: `face-detection-`_your-name_ (you created this bucket earlier)
- Event type: `Object Created`
- Prefix: `faces/`
- Filter: `.jpg`
- Enable trigger: ON (keep the checkbox on)

Save the Lambda function.

Under Actions tab choose **Publish**.

**Step 4- View the emotions on a dashboard**

Go to [AWS Management console](https://console.aws.amazon.com/console/home?region=us-east-1) and search for Cloudwatch

- Create a dashboard called `sentiment-dashboard-`_your-name_
- Choose Line in the widget
- Under Custom Namespaces, select “string”, “Metrics with no dimensions”, and then select all metrics.
- Next, set “Auto-refresh” to the smallest interval possible (1h), and change the “Period” to whatever works best for you (1 second or 5 seconds)

NOTE: These metrics will only appear once they have been sent to Cloudwatch via the Rekognition Lambda. It may take some time for them to appear after your model is deployed and running locally. If they do not appear, then there is a problem somewhere in the pipeline.


### With this we have come to the end of the session. As part of building this project, you learnt the following:

1.	How to build and train a face detection model in SageMaker
2.	Modify the DeepLens inference Lambda function to upload cropped faces to S3
3.	Deploy the inference Lambda function and face detection model to DeepLens
4.	Create a Lambda function to trigger Rekognition to identify emotions
5.	Create a DynamoDB table to store the recognized emotions
6.	Analyze the collected data using CloudWatch
