This guide demonstrates how to build a Box Skill application in Node.js using Serverless, a command line tool for building and deploying applications to serverless architectures, and the Box Skills Kit, a library for interacting with the Box API and integrate it with AI/ML services from Google Cloud !

Please follow the instructions in https://github.com/box/box-skills-kit-nodejs/tree/master/boilerplate-skills to deploy a Google cloud function using Serverless !. You can also follow instructions @ https://cloud.google.com/functions/getting-started/ to using google native tools.

Things to note: 
      1. Please ensure you replace the serverless.yml in the instructions above with the yaml file from this repo.
      2. Google cloud functions automatically parses JSON string to objects, you may have to edit the line 131 in the skills-kit library from 
        function FilesReader(body) {
          const eventBody = JSON.parse(body);
          ....
      }
    
    to 
      function FilesReader(body) {
        const eventBody =body;
        ....
      }
      
      
Setup on Google Cloud:
Please follow instructions at https://cloud.google.com/vision/product-search/docs/quickstart to setup product search catalog.
Ensure you have a project in GCP and billing enabled !. 

About Product Search

Cloud Vision Product Search allows retailers to create a set of products, each containing reference images that visually describe the product from a set of viewpoints. Currently Vision API Product Search supports the following product categories: homegoods, apparel, and toys.

When users query the product set with their own images, Vision Product Search applies machine learning to compare the product in the user's image with the images in your product set, and then returns a ranked list of visually and semantically similar results.

The quickstart demonstrates how to create a product set which contains a group of products with reference images for those products. The quickstart shows users how to create a product set, products, and their reference images in a single step by batch import. After the product set has been indexed, you can query the product set using Vision Product Search.

We will use Product search api's within our cloud function, which gets triggered when a file is uploaded into Box.

The use case is: You, a retailer, use Box for storing all your product  related data such as images. There are a lot of images to organize and you need a quick way to not only organize these datasets but also find out similar products, the max price of such products and other information.
You choose to create a ML powered product catalog in Google Cloud, which allows you to query visually and semantically similar items. Once you upload the data into Box, the custom skill that you've built will call the Google Cloud Product Search api - the catalog for which you;ve built already - The API returns similar product in your catalog and the category, price information.

