---
title: "Azure Custom Vision Services"
date: 2018-08-06T13:54:23Z
draft: false
tags: ["azure","cognitive services","vision"]
---

**Custom Vision**

Azure Custom Vision is a different service to Azure Computer Vision.

Custom Vision focuses on object detection & image classification using a custom built model, this means training images need to be prepared and uploaded.

The real beauty of custom vision is its ease of use and the powerful models which can be built. The majority of the work is in preparing and tagging the classifier images and uploading to the web portal.

The quick start guide describes how to use service with the .Net SDK, Python and Java SDK are also available as well as a REST API.

Once the images are uploaded and the model is trained the model can be access via an HTTP API call - Using the Prediction API.

**Exporting the Model**

Once a classifer model is built in Custom Vision ai it can be exported as a Tensorflow (Android), CoreML(iOS11), ONNX(Windows) or a Windows/Linux Container which can be used on mobile devices. These are compact models which can be shipped with the application and will allow the images to be processed off line. 

**C# API Call Example**

The sample below shows an alternative method using the Custom Vision NuGet Package to upload and image and get a collection of predictions back.

{{< highlight csharp>}}

 using System;
 using System.Collections.Generic;
 using System.IO;
 using System.Linq;
 using System.Threading.Tasks;
 using Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction;
 using Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction.Models;
 using Microsoft.Bot.Builder.Dialogs.Internals;

 namespace SampleApp
 {
    public class ImagePredictionService
    {
        public static async Task<PredictionModel> MakePredictionRequest(Byte[] imageBytes)
        {

            string predictionKey = "<Replace with Key>";

            PredictionEndpoint endpoint = new PredictionEndpoint() { ApiKey = predictionKey };

            try
            {
                var predictionReturn = new PredictionModel();

                using (var stream = new MemoryStream(imageBytes))
                {
                    var result = endpoint.PredictImage(Guid.Parse("<Iteration GUID"), stream,
                        Guid.Parse("<Replace with GUID>"));

                    predictionReturn = result.Predictions.MaxBy(x => x.Probability);                   
                }
                return predictionReturn;
            }
            catch (Exception ex)
            {
                return null;
            }

        }
    }
 }

{{< / highlight >}}

**Demos & Samples**

[https://github.com/Microsoft/Cognitive-Samples-IntelligentKiosk](https://github.com/Microsoft/Cognitive-Samples-IntelligentKiosk)

[https://github.com/Microsoft/Cognitive-Samples-IntelligentKiosk/blob/master/Documentation/EmotionAPIPlayground.md](https://github.com/Microsoft/Cognitive-Samples-IntelligentKiosk/blob/master/Documentation/EmotionAPIPlayground.md)

[https://github.com/Microsoft/Cognitive-Samples-IntelligentKiosk/blob/master/Documentation/RealtimeCrowdInsights.md](https://github.com/Microsoft/Cognitive-Samples-IntelligentKiosk/blob/master/Documentation/RealtimeCrowdInsights.md)

**Services**

[https://azure.microsoft.com/en-us/services/cognitive-services/face/](https://azure.microsoft.com/en-us/services/cognitive-services/face/)

[https://azure.microsoft.com/en-us/services/cognitive-services/content-moderator/](https://azure.microsoft.com/en-us/services/cognitive-services/content-moderator/)

**Use Cases**

[https://towardsdatascience.com/using-object-detection-for-complex-image-classification-scenarios-part-1-779c87d1eecb](https://towardsdatascience.com/using-object-detection-for-complex-image-classification-scenarios-part-1-779c87d1eecb)  