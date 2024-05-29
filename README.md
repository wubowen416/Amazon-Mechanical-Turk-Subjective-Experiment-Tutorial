# Amazon Mechanical Turk Subjective Experiment Tutorial
This tutorial begins with nothing to the end of publishing of a experiment in Amazon Mechanical Turk (AMT).
We will start from the creation of an Amazon Web Services (AWS) account, using which an AMT project will be created.
In the project, a webpage is used as the interface to the participant.
One can edit the webpage using HyperText Markup Language (HTML) for specific experimental purposes, such as adding questions or media.
We assume that the media will be stored in AS3 (Amazon S3), which will also be mentioned in detail.
To test whether everything is correct, or to conduct a preliminary study, AMT Sandbox (Sandbox) is the best tool. 
Finally, the experiment can be published through AMT, and we can wait for the responses.

## Requirements
- An email address
- A phone number
- A credit/debit card, though you will not be charged
- Very basic knowledge of HTML for webpage design

## Abbreviations
| Abbr. | Full name |
| --- | --- |
| AWS | [Amazon Web Services](https://aws.amazon.com) |
| AMT | [Amazon Mechanical Turk](https://www.mturk.com) |
| HIT | [Human Intelligent Task](https://blog.mturk.com/tutorial-understanding-hits-and-assignments-d2be35102fbd) |
| HTML | [HyperText Markup Language](https://en.wikipedia.org/wiki/HTML) |
| AS3 | [Amazon S3](https://aws.amazon.com/s3/) |
| Sandbox | [AMT Sandbox](https://requester.mturk.com/developer/sandbox) |

## Table of Contents
- [Preliminaries](#Preliminaries)
- [Creation of AWS Account](#Creation-of-AWS-Account)
- [Test in Sandbox](#Test-in-Sandbox)
- [Publishing Experiment in AMT](#Publishing-Experiment-in-AMT)
- [AS3 as Data Storage](#AS3-as-Data-Storage)
- [Tips on Preparing Materials](#Tips-on-Preparing-Materials)

## Preliminaries
### HIT and Assignment
HIT and assignment are important concepts in AMT and will be frequently used throughout this tutorial.
It is better to grab their meaning in the context of AMT before proceeding.

In general, a HIT refers to the task that the workers on AMT (the participant to your experiment) will complete.
Assignemnts are be published onto AMT for workers to complete.
Usually, we will publish one assignment for each HIT to obtain one response for each HIT, but sometimes we want to collect more than one response for each HIT.
In this case, we can publish multiple assignments for each HIT to obtain multiple responses for each HIT.
These assignments will be assigned to different workers to ensure the responses are from different sources (theoretically).

As a concrete exmaple, assume that we want to collect the category for a number of images, say 3 images.
In this case, the classification of one image would be one HIT.
In total, there will be 3 HITs.
If we want only one response for each image, we can publish only one assignment for each HIT.
But if we want multiple responses, we can publish multiple assignments for each HIT.
Therefore, if we publish 100 assignments for each HIT, the total number of assignments will be `3x100=300`.
We will receive `3x100=300` responses, including 100 reponses for each image.

For more information on this topic, please refer to [here](https://blog.mturk.com/tutorial-understanding-hits-and-assignments-d2be35102fbd).

## Creation of AWS Account
You will not need to use your own account if the lab provides an official account for you because they will pay the fee.
However, it is better for testing the experiment using Sandbox, in which case you still need to use your own account. 
The following procedure shows how you can create an AWS account using an existing email address.

1. Navigate to [AWS](https://aws.amazon.com) and click on `Sign In to the Console`.
<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/dbaa7215-cd9f-4cae-8174-69b7f132e934">

2. Click on `Create a new AWS account`.
<img width="200" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/32582e48-f0f9-43fa-ab4b-5d6adf6b105a">

3. Input email address and account name whatever you want, and follow their instructions to complete the sign up, which requires password, contact information, a credit/debit card, and a phone number. Finally, choose the `Basic support - Free` to complete.

## Test in Sandbox
Sandbox is free to test the experiment.
It will not charge the requesters who publish assignments.
Also, it will not pay the workers for completing any assignment.

In a word, we login as requester to the Sandbox to create a project and pubulish assignments, and login as worker to complete our published assignments.

The following shows how to achieve this:
- [Login as Requester](#Login-as-Requester)
- [Creat Sandbox Project](#Creat-Sandbox-Project)
- [Publish Assignments](#Publish-Assignments)
- [Complete Published Assignments](#Complete-Published-Assignments)

### Login as Requester
Navigate to [AMT-Sandbox for requester](https://requester.mturk.com/developer/sandbox) and click on `Requester Sandbox`. 

<img width="200" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/3c4c0a08-6760-437c-8b1b-c3ca75f09f98">

Sign in using your AWS account.
If this is the first time you use AMT, you will be creating a new AMT account.

<img width="400" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/e0b0f192-b4d2-44a1-b75a-d40b3152625d">

A display name and input your email will be required. 
The contact email can be the same as AWS email address.
Input them and create the account.

<img width="400" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/3b3c5553-b030-4f30-a106-a728981302c9">

After login, check if this is the sandbox. 
A banner will be on the top of the page as an indication.

<img width="400" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/d9fb9202-30b0-4113-8226-18bb42ca7986">

If you are not in Sandbox, navigate to [AMT-Sandbox](https://requester.mturk.com/developer/sandbox) and sign in using the account just created.

### Creat Sandbox Project
We take the classification of a number of images as an example to show how a Sandbox project can be created.

The reason is that usually we would have workers eavalute images, audios or videos, which need to be stored somewhere on the cloud and loaded to the assignment to be visible to workers, via a csv file containing the url of them.
Therefore, it is necessary to explain how the csv file should look like.
Image classification can be a minimal example to demonstrate how to achieve this.
If your experiment does not contain anything that needs to be loaded from cloud sources, you do not need to provide the csv file. You can skip the part that concerns the csv file.

#### Enter Properties
Click on `Create` tag, and select `Image Classifcation` in Vision category, fianally click on `Create Project`.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/7cf7097f-cf80-40f0-a8b4-0382f3c8eb8c">

You will have to enter the following for creating a project:
- `Project Name` is the name for you project managemtnt. It will only be shown to you.
- `Title` will be shown to all workers on AMT (Sandbox in this case). Choose a unique title, so that it can be easily distinguished from other assignments, for us to search afterwards. I usually use my name and the current date and time, e.g., WuBowen-20240528-1553. However, in the real experiment, the title should be informative of your task for gathering participants.
- `Reward per assignment` is the amount you will pay for each assignment. We set to 0.0 because this is only for test.
- `Number of assignments per task` is how many responses you want for each HIT. We will set to 1 for testing.
- `Time allotted per assignment` is the time limitation for completing one assignment.
- `Task expires in` is the duration of how long your task will last for workers to see and accept.
- `Auto-approve and pay Workers in` means if you do not approve or reject a response for a period of time, it will be automatically approved, so that the reward will be given to the worker who has completed this assignment. This will not happen in the Sandbox.
- `Require that Workers be Masters to do your tasks`. AMT maintains a list of wokers who show high performance. Check to only allow Masters to complete your task. Although this is likely to improve the quality of the responses, more completion time is generally expected. Do not check Yes in Sandbox because you will not be able to test it using your non-Master account.
- `Specify any additional qualifications Workers must meet to work on your tasks` provides creterions to filter out workers who do not meet. For example, sometimes we want our participants to be located in some contries. In our case, we can set the region of workers to  Japan.
- `Task Visibility`. I do not really understand the purpose of this option. Usually keep it `Public` will suffice.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/dc63fd7b-3a0d-4aa9-9c0f-541253fa5da4">

Finally, we can proceed to design the layout.

#### Design Layout
You will be presented with a template of HTML code, which defines the interface of the experiment.

While you can edit the content for you specific purpose, one thing requiring attention is how to load images in to this HTML.
In the code, there is a tag called `crowd-image-classifier` in the red box, as shown in the following figure.
While it has four attributes, the `src` variable is crucial for loading images.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/2084a2fa-fcbd-485c-b32e-73b6f5456b8b">

For image classification, when publishing a batch of assignments, a csv file is required to provide the urls to those images.
As an example, our csv file contains a column named by `image_url`, followed by rows of an url of an image, which looks like this:

| image_url |
| --- |
| url of image 1 |
| url of image 2 |
| url of image 3 |

When creating HITs, one row will be used to create one HIT.
If there are 3 rows excluding header, 3 HITs will be created in total.
All HITs will be created using the same HTML code.

In the HTML code shown in the above figure, the value of `src` defines the url to image.
`src="${image_url}"` means that `src` will take the value under the column named by `image_url` in the csv file.
For our example csv file, when creating the first HIT, `url of image 1` will be filled to `src`, and when creating the second HIT, `url of image 2` will be filled to `src`, and so on.

By changing or adding urls in the csv file, we can choose the images we want to classify.
In addition, you can have multiple columns for loading other data if you want.
You can refer to their url in the csv by `${YOUR_COLUMN_NAME}` in HTML.
For advance usage, you can browse other project templates and read the comments in it.

When finised, click on the `Preview` to proceed to the next step.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/e3b05af2-e058-423f-ac45-610406635bb6">

#### Preview
In the preview page, we can check if the page is rendered as intended.
Ignore the warning `Failed to load the image` because we have not provided csv for it to load the images.

You can click on the page to test each functionality.
For example, cliking on instruction will show a window of instruction.
These are connected to HTML elements in the source code.
You can go back and modify the code if anything is wrong.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/02b79811-f736-464b-8e3a-5250023e4a05">

You can submit an answer in this preview and see what results you can get.
Select one option and click on the submit at the bottom right.

<img width="400" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/5e5b613e-6f4f-417a-8aaa-9117f7d2d99a">

Your answer will be shown on the top of the page.

<img width="400" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/340af974-dede-4806-a198-2751ae8aedab">

If everything is alright, click finish.

### Publish Assignments
#### Prepare Csv File
The format of the required csv file has been described in [Design Layout](#Design-Layout).
[Here](https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/files/15466602/input.csv) is a template csv file I created for demonstration purpose.
You can download it and check its content to get a sense, or you can also make your own csv file.

As for the place to store the data, there should be numerous ways to assign an url to experiment materials, through which the data can be accessed from all over the world.
In this tutorial, we show how to achieve this using AS3 in [AS3 as Data Storage](#AS3-as-Data-Storage).
In the following, we assume a valid csv file has already been created.

#### Publish a Batch of Assignments
After the csv file is prepared, click on `Publish Batch`.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/50317095-3e1e-4556-ba50-1757a5f964f5">

Choose a csv file.

<img width="300" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/1fe90bf4-f994-4aa3-bade-22556e6cc8a6">

Upload the file.

<img width="300" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/e6729cb6-5bae-4ec8-8d83-a220230c76d3">

Sandbox allows you to preview the task before publishing it.
Below shows some elements you may want to check:
- Left upper corner shows the title.
- `Reward` shows the reward to workers who has completed an assignment. It is 0 as we set it to 0.
- `Tasks Available` shows how many assignments are there that one worker can accept and complete. This is 3 as our csv files contain 3 images. Note that although we can publish multiple assignments for each HIT, which will result in assignments more than 3, each worker can only complete one set of HITs, which is 3. So this number should be equal to the number of rows in the csv file.
- `Duration` shows the time limitation for completing the assignment.
- `Showing Task 1 of 3` shows the progress of HITs.
- `Next HIT` in our case is used to go to next image, i.e., the next row in the uploaded csv file.
- `Qualifications Required`. The criterion we have set.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/4d9656e0-ff20-4b34-8deb-f9d25479cb1b">

Check the information of the batch.
You can change the `Batch Name` for management of your batches.
The `Cost Summary` can be ignored since we are in Sandbox.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/1a3bf401-8fc2-4c5e-9bee-486430fe5432">

I feel like more explanation is needed for `Tasks` as the description is not so comprehensive.
`Number of tasks in this batch` refer to how many assignments are there that one worker can accept and complete, in our case it is 3.
`Number of assignments per task` refer to the number of assignments we publish for each HIT, in our case it is 1.
As a result, `Total number of assignments in this batch` is the total number of assignments, in our case `3 (assignments for one worker) * 1 (number of assignment per HIT) = 3`.

Click on `Publish` to publish the assignments.

Immediately, the page should be redirected to batch details, where you can check status of the batch, and view the results.
- `Assignments Completed` shows the progress.
- `Cancel` can terminate the publishing of assignments. However, assignments that have already been accepted by workers will not be terminated.
- `Results` is where we can check the received responses of workers.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/51669560-5347-443e-abe6-da87f9a3d862">

### Complete Published Assignments
#### Login as Sandbox Worker
Navigate to [AMT-Sandbox for worker](https://workersandbox.mturk.com/), login use your Amazon account.

In order to accept and complete an assignment, an Amazon account for AMT worker needs to be registered.
Create your Amazon account first if you do not have one.
You can use the email used to create the AWS account for the registeration.

<img width="200" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/47af8313-d705-4ff9-94cf-c4718633dbe1">

There should be a banner on the top of the page to indicate this is the sandbox.
If there is no one, navigate to [AMT-Sandbox for worker](https://workersandbox.mturk.com/).

<img width="400" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/f89ee4ad-5f76-4d50-af9b-4657b97a97bd">

In Worker Registeration, input necessary information and click on `Create Account`.

#### Browsing Published Assignments
Because we want to complete the assingment published by ourself, we can search for it by inputting the title. In our case, it would be `WuBowen-20240528-1553`. The search results are shown below.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/15573b46-64f6-4a96-8cd8-0d512ff020ce">


#### Complete the Assignment
Click on `Accept & Work` on the right of the assignment to proceed.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/44c89d8f-9437-45ad-8407-1e654272c2cb">

Then you can submit your answer to complete the assignment.
Select one category and submit the answer.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/d580233a-126d-405d-ba2f-4f4c605da0bf">

If there are multiple HITs, you need to accept each of them before complete it.
Checking the `Auto-accept next HIT` can improve the efficiency.

Note that one Amazon account can only accept the one set of HITs. 
In order to complete multiple set of HITs, prepare multiple accounts in advance.

### Examine Results
Now we can go back to the requester Sandbox to check the results.

Login as requester, navigate to `Manage` tag, the published batch will be there.
Click on `Review Results` to view the results.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/bc7514b3-edfe-4936-8d85-cf560c2ee25e">

The table shows all the received responses that have not been approved or rejected.
The results can be downloaded as csv and used for data analysis.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/740e205f-0aab-4a1b-8513-ba4b1754fab1">

In real AMT experiment, you can check the response of each worker, and decide to approve or reject their response. 
This is necessary as there will be bots or people that give low-quality responses which can bias the result. 

By approving a response, you give permission to reward the worker.
If you reject, the workder will not be paid, and AMT will automatically publish a new assignment for that HIT.

By downloading the csv, and mark "x" under a column titled "Approve" or putting your reject comment under  a column title "Reject", you can do this offline.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/8cbbe96d-63c4-401f-a159-2fc4395d6839">

Afterwards, you can upload this edited csv to AMT for this purpose.

<img width="300" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/e544678f-b832-44cf-8f95-503d7b9973c6">

## Publishing Experiment in AMT
Basically, the same procedure described in [Creat Sandbox Project](#Creat-Sandbox-Project) and [Publish Batch of Assignments](#Publish-Batch-of-Assignments) can be followed, except the setting of [Reward, Number of Assignments, and Cost Summary](#Reward,-Number-of-Assignments,-and-Cost-Summary). 

Other minor changes are as follows:
- **Login portal**. We login to [AMT](https://requester.mturk.com/) instead of Sandbox.
- **Title**. Different from Sandbox, the title should be informative about the task that the particpants will do in the experiment to gather relative workers more efficiently. For example, if the task is the image classification, the title could be: Picking the best category for images.

### Reward, Number of Assignments, and Cost Summary
Let us clarify the meaning of these words first.
`Reward` refers to `Reward per Assignment` in the `Enter Properties` section.
The `per Assignment` in `Reward per Assignment` is equal to `per HIT`.
Therefore, this is how much you will pay the workers for completing **one HIT**.
For example in our image classification experiment, if we set the reward to $5, workers will receive $5 for classifying **one image**.
For demonstration, we will set the `Number of assignments per task` to 100, which means we want to gather 100 responses for each HIT.

<img width="300" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/781874de-8ef5-4bfc-acc4-25442a016d5a">

Recall that we have 3 images to classify (3 HITs), the total number of assignments would be `3x100=300`. 
In the confirmation page (as shown below) before publishing the batch, the `Total number of assignments in this batch` should be 300.
The `Estimated Total Reward` would be the `Reward per Assignment` times the total number of assignments, which is `$5x300=$1500`.
`Estimated Cost` shows the estimated total amount of money you will need to pay, including to the workers and to Amazon. 

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/7b94285b-ca9d-44e0-a9d8-32348afffba9">

#### Montly Limitation
There is a warning on exceeding montly credit limit. 
It is unclear what is the default limit, but if you want to increase it, contact customer service of AMT or Amazon. 
I successfully raised my limit to $1000 before. 
I will share how I achieved this in the future.

## AS3 as Data Storage
Every newly registered AWS customer can receive 5GB of AS3 storage [for free](https://aws.amazon.com/s3/pricing/?loc=ft#AWS_Free_Tier).
This is a good place to store our data if the scale is not that large.
The rest of this section show how to store your data in AS3 and obtain their url for the access from all over the world.
While we only show a minimal example, you can change specific settings for you own purpose.

### Login to AS3
Navigate to [AS3](https://aws.amazon.com/s3/) and click on `Sign In to the Console` using your AWS account.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/0b24a7f7-4b2e-43ad-851b-f99053d42017">

### Create Bucket
On top of the page, search for S3 and click on `S3`.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/dcdb09bb-5936-467d-9865-c4127a0d76ef">

Click on `Create a Bucket`.

<img width="200" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/4556febf-01ee-45dc-93b3-c7e3065b6864">

Input a bucket name.
The bucket name should be unique globally on the internet because we want to use its url.
AS3 will check for this after your input.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/015924c9-a6f1-4cb2-90fa-964eb6640690">

Change object ownership to `ACLs enabled` so that the content can be made public afterward.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/2958818a-28c1-483f-b8c5-f270d6a36675">

Uncheck `Block all public access` to allow access from public.
Check the consent below.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/8c0e1be3-3394-4ca9-93c1-7eba41d2e364">

Go to the end and click on `Create bucket`.

<img width="200" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/bdd5d363-e21a-43c2-997d-380fd62a497f">

### Upload Data
Immediately, you should be redirected to the list of your buckets.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/eeee60c7-637c-4908-9bc7-65d466e9de04">

Click on the bucket name to view the details of the bucket.

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/737ed80a-1192-4d6e-a8e9-5cbb1cf1597d">

By clicking on the `Upload`, you can upload files.
Add your files or folders.

We will upload a folder called demo-folder, which has the following structure:
```
demo-folder
|--demo-folder-inside-1
|  |--demo-image-1.jpeg
|  |--demo-image-2.jpeg
|--demo-folder-inside-2
   |--demo-image-1.jpeg
   |--demo-image-2.jpeg
```

The page should look like this:

<img width="500" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/6cc3db27-fff1-438c-bbb7-d1c0d3146b44">

Click `Upload` to proceed.

AS3 will show the results of uploading.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/47576cc1-9b19-49c6-aaed-a81477a6d652">

Click `Close` on the right upper corner to go back to the bucket.

### Making Public

By default, these files are not public.
Although there is a link for each file, it is not available to access.
In order to make these files public, check the items and click on `Make public using ACL` in the drop down menue of `Actions`.

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/cbf8748b-d6d5-4fd9-afd0-efa83c2d7b26">

Click on `Make public` in the next page.
AS3 will show the results of making public.

### Obtaining Url

Navigate to any uploaded file and click on the file name to view the object overview.
The `Object URL` shows the url to access this specific object.
You can use this link to prepare the csv file for publishing assignments described in [Prepare Csv File](#Prepare-Csv-File).

<img width="600" alt="image" src="https://github.com/BowenWuResearch/Amazon-Mechanical-Turk-Subjective-Experiment-Tutorial/assets/170743218/1e7ffa24-e1a9-4675-85e4-c6784d11ff96">

You will not be able to access to view the item because my bucket has already been deleted.

You may have already noticed that the postfix of the url is the same as the structure of the folder we uploaded, which is `demo-folder/demo-folder-inside-1/demo-image-1.jpeg`.
In fact, the url in AS3 preserves the directory structure in the uploaded folder.
This makes it easy for creating the csv file when we have multiple files.
We can recursively obtain the full path to each file in the directory locally, and append them with the prefix of AS3 path, which in our case is `https://demonstration-20240529-1726.s3.ap-northeast-3.amazonaws.com/`.

## Tips on Preparing Materials
### Multiple Items in one HIT
By publishing assignments, we will be charged by Amazon as the management fee.
Therefore, we would like to keep the number of assignments as small as possible.

The method would be including multiple items in one HIT.
For example, in image classification, instead of classifying only one image in one HIT, we can put 10 images in one HIT.
Therefore, if we have 100 images, 10 assignments would be sufficient rather than 100.
This can significantly reduce the cost.

However, this will result in less variation of workers.
While for a between-subject design this must not be done, it is necessary for within-subjective design.

### Including Attention Check Questions
There are so many bots on AMT.
There are also people who do not give responses carefully.
These can significantly affect the analysis of data.

It is common or even mandatory to include attention check questions to filter them out.
Simple yet effective way is expected to achieve this.
For example, in the image classification task, we can check some answers of a specific worker.
If significant mistakes are being made frequently, we can remove the data, or reject the response on AMT.

For comparison tasks, for example compare two generated audio which is natural, we can make one of them white noise.
If someone chose the noise, we can filter out the response.
Because a random guessing will be correct half of the time, we can use more attention check questions to lower its probability.
For instance, 3 questions can lower the probablity to `1/8`, which I believe is sufficiently low.

### Obtaining the Consent from Workers
For acadamic research, it is mandatory to obtain consent from the participants before the experiment.
There is a `return` button after the acceptance of an assignment.
By clicking on it, the acceptance will be withdrawned, and the assignment will be republished.

In the first page, we should describe the content of the experiment, and notify the workers that we will collect their answer for data analysis.
If you want to collect personal information such as age and gender, you should mention it clearly.
If they do not agree, they can click on `return` to withdraw the acceptance.

## Contact
My email: wu.bowen.dp@gmail.com

Feel free to open an issue for anything.
