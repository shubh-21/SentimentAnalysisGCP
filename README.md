# What is Sentiment Analysis ?
Sentiment Analysis is a Natural Language Processing (NLP) technique used to determine the sentiment expressed in a piece of text. It classifies text as **positive**, **negative**, or **neutral** by analyzing words, phrases, and context. </br>
Common Applications includes : </br>
* Customer Feedback Analysis
* Social Media Monitoring
* Opinion Mining

Machine learning models, deep learning techniques, or pre-trained APIs like GCP Natural Language API can be used for sentiment analysis. </br>
We will be looking at GCP Natural Language API approach for Sentiment Analysis.

## GCP Natural Language API
The Google Cloud Natural Language API is a cloud-based service that helps developers analyze and interpret text using machine learning. It offers various NLP features, including: </br>
* **Sentiment Analysis** – Evaluates whether the text conveys a positive, negative, or neutral emotion.
* **Entity Recognition** – Detects and categorizes key entities such as names, places, and dates.
* **Syntax Analysis** – Examines sentence structure, grammar, and parts of speech.
* **Content Classification** – Assigns text to relevant categories.
* **Entity Sentiment Analysis** – Identifies entities and assesses their associated sentiment.

### Requirements:
* Google Cloud Platform Project
* Browsers (Eg: Chrome, Firefox)

### Steps to follow: 
#### 1. Setup Account and Project </br>
- Before you begin, ensure you have a Google Account and are signed in to the **Google Cloud Platform Console**.  
To create a new project, navigate to the **Manage Resources** page and click **CREATE PROJECT**.
- Take note of your **Project ID** as displayed in the screenshot. Additionally, ensure you provide a unique **Project Name**.
- We have given Project Name as "Sentiment". </br>
<img  src="https://github.com/shubh-21/SentimentAnalysisGCP/blob/main/SentimentGCP/1.png">


 #### 2. Configuration </br>

With your account and project setup complete, the next step is to configure your project for the **Google Cloud Natural Language API**.  
- Open the **Dashboard** menu and select **APIs & Services**.  
- Click on **Enable APIs and Services**.  
- Search for **Google Cloud Natural Language API** and select it.  
- Click **ENABLE** to activate the API.
- 
After a few seconds, the API should be successfully enabled. </br>

<img src="https://github.com/shubh-21/SentimentAnalysisGCP/blob/main/SentimentGCP/2.png">

#### 3. Activating Cloud Shell </br>

**Google Cloud Shell** is a command-line environment for managing resources on **Google Cloud Platform (GCP)**. It runs in the cloud and allows you to execute commands directly.  

We'll use **Cloud Shell** to send requests to the **Natural Language API**.  

- Click on the **Activate Cloud Shell** icon in the top right corner of the header bar.  
- A **Cloud Shell session** will open in a new frame at the bottom of the console, displaying a command-line prompt.  
- Wait until the `user@project:~$` prompt appears, indicating that the session is ready. </br>

#### 4. Create an API Key
To interact with the **Natural Language API** using `curl`, we need to generate an **API Key**. Follow these steps:  

- Open the **Google Cloud Console** and navigate to **APIs & Services > Credentials**.  
- Click on **Create Credentials** and select **API Key**.  
- A pop-up will display your newly generated API Key. Copy it and store it securely.  

Now, switch back to **Google Cloud Shell** and run the following command:  

```bash
export API_KEY=<YOUR_API_KEY>
```

Replace `<YOUR_API_KEY>` with the key you copied earlier. This command stores the API key in an environment variable, so you don’t need to include it in every request.

<img src="https://github.com/shubh-21/SentimentAnalysisGCP/blob/main/SentimentGCP/3.png">

#### 5. Sentiment Analysis Using GCP Natural Language API
Now we’re ready for the exciting part—where the machine learning magic happens with the **Natural Language API** for **Sentiment Analysis**.  

- **Create a JSON Request**:  
   First, create a JSON file with the text you want to analyze. This can be done in your **Cloud Shell** environment. You can use any command-line text editor (e.g., nano, vim, emacs) or the built-in **Orion editor** in Cloud Shell.  

   To use the Orion editor:  
   - Open the editor by clicking **File > New > File** and name the file `request.json`.  
   - Copy and paste the following JSON content into the file:  

```json
{
  "document": {
    "type": "PLAIN_TEXT",
    "content": "Inception is one of the best movies of all time. I think everyone should watch it."
  },
  "encodingType": "UTF8"
}
```

- **Request Explanation**:  
   - The **type** field specifies the format of the text (PLAIN_TEXT or HTML).  
   - **content** contains the text that will be analyzed by the API.  
   - **encodingType** sets the text encoding to UTF-8.  

   If you wish to analyze a file from **Cloud Storage** instead, replace `content` with `gcsContentUri` and provide the URI of the text file in Cloud Storage.

Once you have created the `request.json` file, it’s ready to be used in a request to the **Google Cloud Natural Language API** for sentiment analysis. </br>

To perform **Sentiment Analysis** with the **Google Cloud Natural Language API**, run the following `curl` command in your Cloud Shell:

```bash
curl "https://language.googleapis.com/v1/documents:analyzeSentiment?key=${API_KEY}" -s -X POST -H "Content-Type: application/json" --data-binary @request.json
```

The response will contain two key parts:  

- **documentSentiment**: The sentiment for the entire block of text.  
- **Sentence-level Sentiment**: Sentiment for each sentence, with two key values:  
  - **Sentiment Score** (from -1 to +1): Indicates sentiment, where -1 is negative, +1 is positive, and 0 is neutral.  
  - **Magnitude**: Represents the strength of the sentiment (range: 0 to infinity).  

For example, a score of **0.5** with a magnitude of **1.1** indicates a moderately positive sentiment for the document. The first sentence might have a **score of 0.9** (strongly positive), while the second sentence might have **0.1** (slightly positive).

<img src="https://github.com/shubh-21/SentimentAnalysisGCP/blob/main/SentimentGCP/4.png"> 

#### 5. Experimenting With Positive, Negative and Neutral Sentiments
To test Sentiment Analysis with some other statements, follow these steps:

- Go back to your request.json file in Cloud Shell.
- Edit the file to include some other feedback.
- Save the changes to your file. </br>

- Positive
  
  <img src="https://github.com/shubh-21/SentimentAnalysisGCP/blob/main/SentimentGCP/pos.png">

- Negative
  
  <img src="https://github.com/shubh-21/SentimentAnalysisGCP/blob/main/SentimentGCP/neg.png">

- Neutral

  <img src="https://github.com/shubh-21/SentimentAnalysisGCP/blob/main/SentimentGCP/mid.png">
