# Tidy-Tabs-Summary
Condense your Browser Tabs into a few impactful words. - Inspired in Arc Max

Here are some examples you can try that aren't included in the training or test datasets
# Test the 3 models Online
[Hugging Face Space](https://huggingface.co/spaces/wgcv/Tidy-Tabs-Titles) 

# Examples
```
Urls:
High Similarity to Training Data:
https://www.nytimes.com/2007/01/10/technology/10apple.html
https://www.nytimes.com/2021/04/15/arts/design/Met-museum-roof-garden-da-corte.html
https://github.com/torvalds

Less than 2% Overlap with Training Data:
https://substack.com/browse/staff-picks/post/145699191
https://brentcates.substack.com/p/julian-assange-is-now-free-to-collapse

Moderate Similarity to Training Data:
https://techcrunch.com/2024/07/05/openai-breach-is-a-reminder-that-ai-companies-are-treasure-troves-for-hackers/
https://www.forbes.com/sites/davidphelan/2024/07/09/apple-iphone-16-pro-major-design-upgrade-coming-new-report-claims/
https://www.crn.com/news/channel-programs/18828789/microsoft-to-release-windows-xp-service-pack-1
https://www.rickbayless.com/recipe/pastor-style-tacos/

No Similarity to Training Data:
https://www.notioneverything.com/blog/notion-note-taking-templates
https://www.eluniverso.com/noticias/ecuador/quito-prohibido-circular-dos-personas-moto-seguridad-nota/
https://www.swift.org/blog/swift-on-windows/

    Some websites, like x.com or instagram.com, are not accessible because they use JavaScript engines to load content, which is beyond the scope of this project. 
    Feel free to try any URL 🧪🌐


```
            
# The Dataset
The project's creator collected the dataset from various sources on the internet. 
The dataset includes: 
            
| Feature                    | Description                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------|
| URL                        | URL of the webpage                                                                            |
| title                      | Extracted from the HTML `<title>`                                                             |
| description                | Extracted from `<meta name="description" content="description">`                              |
| paragraphs                 | Extracted from `<p>` tags                                                                     |
| headings                   | Extracted from `<h1>`, `<h2>`, `<h3>` tags                                                    |
| combined text              | Formatted as `[title] title \\n [description]description`                                     |


The dataset primarily comprises data gathered from nytimes.com and GitHub.com, supplemented by approximately 60 other websites featuring diverse content. From GitHub, 1226 summaries were created programmatically, creating the summary with the format Username GitHub Profiles to explore the model's ability to generate patterns with new words. For the New York Times, 1056 websites were summarized based on their text content, using Claude 3.5 Sonnet of Anthropic with a specified prompt.
## Prompt for labels Generation
```
        Claude 3.5 Sonnet Prompt
             
            I’m going to share with you a csv file with one column . I want you to create a summary of 1 to 3 words maximum of the text. The text could have HTML tags. The title is the title of the page and the description is the page's description. 
            The result gives me like this 
            ``` 
            summary 1
            summary 2
            ...
            summary n
            ```
            Only plain text and no additional instructions
```

- This small dataset aims to provide an initial assessment of model performance in a pre-trained task limited to concise summaries of 1 to 4 words. Due to the inherent complexity of this task, I suggest future efforts focus on constructing a larger dataset comprising 50,000 to 500,000 websites to more comprehensively evaluate model capabilities.

- Testing revealed that the description meta tag significantly enhanced result generation. Increasing dataset size and incorporating contextual data are expected to further improve model performance in larger-scale applications with millions of data points.

- Out of the 60 additional websites included, only 41 are sourced from substack.com. This means that less than 2% of the dataset contains information from substack.com. This is valuable for understanding the impact of small data examples.

- P.S. I tested ChatGPT-4.0, and the results were highly discouraging for a chunk of data consisting of 100 text filed values.

-In the future, we should aim to increase the dataset size to at least 10,000-15,000 samples and improve the train/test/validation split methodology.

st.info("I crafted this dataset using a more powerful LLM and scripts, no need for boring manual labeling. The idea is to eliminate human labeling.",icon="ℹ️")

#### Access to the data
            
`https://huggingface.co/datasets/wgcv/website-title-description`

# Models
The objective of the project was to show that it was possible to create a small ML model from a bigger LLM model that could achieve good or better results in specific tasks compared to the original LLM

Given the substantial volume of data, training a model from scratch was deemed impractical. Instead, our approach focused on evaluating the performance of existing pre-trained models as a baseline. This strategy served as an optimal starting point for developing a custom, lightweight model tailored to our specific use case: enhancing browser tab organization and efficiently summarizing the core concepts of favorited websites.

### T5-small
- The [T5-small](https://huggingface.co/wgcv/tidy-tab-model-t5-small) model is a finetuning of google-t5/t5-small.
- It's a text-to-text model.
- It's a general model for all NLP tasks.
- The task is defined by the input format.
- To perform summarization, prefix the text with 'summarize:'.
- 60.5M parameters.
- Disclaimer: The model was retrained once more because poor inference was observed.




### Pegasus-xsum
- The [Pegasus-xsum](https://huggingface.co/wgcv/tidy-tab-model-pegasus-xsum) model is a finetuning of google/pegasus-xsum.
- It's a text-to-text model.
- It's a specialized summarization model.
- 570M params.

### Bart-large
- The [Bart-large](https://huggingface.co/wgcv/tidy-tab-model-bart-large-cnn) model is a finetuning of facebook/bart-large-cnn.
- Prior to our fine-tuning, it was fine-tuned on the CNN/Daily Mail dataset.
- It's a BART model, using a transformer encoder-decoder (seq2seq) architecture.
- BART models typically perform better with small datasets compared to text-to-text models.
- 406M params.


          
### Potential avenues for performance enhancement include:
- Data preprocessing optimization
- Dataset expansion
- Comprehensive hyperparameter tuning
- These strategies could significantly improve model efficacy.
- Add more language in the dataset
### Access to the Models
`https://huggingface.co/wgcv/tidy-tab-model-t5-small`
`https://huggingface.co/wgcv/tidy-tab-model-pegasus-xsum`
`https://huggingface.co/wgcv/tidy-tab-model-bart-large-cnn`

## co2_eq_emissions
- emissions: 0.16 grams of CO2)
- source: mlco2.github.io
- training_type: fine-tuning
- geographical_location: U.S.
-  hardware_used: 1 - T4 GPU
        
## 

