# Performing-OCR-on-scanned-pdf-documents-using-Adobe-Document-Cloud-SDK
This repository provides ways to use Adobe's Document Cloud SDK for performing OCR on scanned pdf documents using Python

Note that Adobe's Document Cloud SDK also provides other services such as:

![EBS Console after hosting](/images/image1.png) 

Among this we will only be using the "Export a PDF" service. This service solves 2 purposes

1. To convert native pdf documents to .docx format.
2. To convert scanned pdf documents to Micorsoft word(.docx) format after OCR conversion . 


At the time of writing Adobe has not release this feature commercially. It is still under public testing phase for early access. But anyone can get acccess to Adobe's Document cloud SDK by giving them a developer request on the following link:
https://www.adobe.io/apis/documentcloud/dcsdk/form.html#:// . 
Once you submit the access request form, a member from Adobe will get in touch with you and provide you the access keys for using the service on an early access basis.This process will take roughly 2 days. Your developer access key that is provided to you will be a json file which is specific to your request. You got to have this json file to use Document Cloud services. The file will be provided to you as "dc-services-sdk-config.json".


# Prerequisites

The sample application has the following requirements:

1. Java JDK : Version 8 or above should be installed on your system.
2. Build Tool: The application requires Maven to be installed. Maven installation instructions can be found here.(https://maven.apache.org/install.html)
3. Now download the sdk folder from this github repository (https://github.com/adobe/dc-services-sdk-java-samples). NOTE: Download this entire repository to your local machine. After download, your repository name would be "dc-services-sdk-java-samples-master". The repository would contain the following files:
              
              --**dc-services-sdk-java-samples-master**
               |_output
               |_dc-services-sdk-config.json
               |_target
               |_src
               |_AUTHORS
               |_CODE_OF_CONDUCT.md
               |_LICENSE.md
               |_pom.xml
               |_README.md
  


4. After you download this repository, replace the file "dc-services-sdk-config.json" with the file you receive from Adobe when you submit the early access request form.


# Build with maven
1. Now navigate to the "dc-services-sdk-java-samples-master" folder in command prompt(for windows) or terminal(for mac or linux).
2. Run the following command to build the project using maven.
```mvn clean install```
3. Now that maven is built, you can start using the PDF to Word OCR service using python.

# Running the service with Python
Before running the python code to convert the scanned pdf to word, 
1. You have to transfer your desired scanned input file that you intend to do OCR on to the directory ```"Your_path_to_dc_services_SDK/dc-services-sdk-java-samples- master/src/main/resources"```. Your file name should be changed to ```"exportPDFInput.pdf"``` and placed inside the "resources" folder.
2. Find the path where maven is installed on your machine. TO find out the path type the following command in your terminal on your machine,```which mvn```.In my case I got the output as:```/usr/local/bin/mvn  #This output might differ from machine to machine depending on the path where maven is installed.```

Now that we have the input scanned pdf file available in "resources" directory as "exportPDFInput.pdf" and the path where maven is installed, we can run the below script in python to convert the scanned pdf document to word document. 

```
import os
java_services_sdk_path = "Your_path_to_dc_services_SDK/dc-services-sdk-java-samples-master"
#Change directory to the "dc-services-sdk-java-samples-master" directory
os.chdir(java_services_sdk_path)  
#Convert scanned pdf to word
os.system("/usr/local/bin/mvn -f pom.xml exec:java -Dexec.mainClass=com.adobe.platform.operation.samples.exportpdf.ExportPDFToDOCX")
```
where ```/usr/local/bin/mvn``` is the path of installation of maven in my machine. You dont have to change any other parameters in the ```os.system()``` command.
Once this command successfully runs, you would have your converted docx file available in the repository ```/Your_path_to_dc_services_SDK/dc-services-sdk-java-samples-master/output/exportPdfOutput.docx```

