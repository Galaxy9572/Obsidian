---
promptId: askGPT4
name: 🗞️Ask GPT-4-Vision (only works with call from another template)
description: Using OpenAI's GPT-4-Vision, describe Image
author: Noureddine
tags:
  - OpenAI
  - markdown
  - gpt-4-vision
  - vision
  - images
version: 0.0.1
disableProvider: true
viewTypes:
  - none
---


```handlebars
You can structure your code here and then use the input or output template to retrieve("get" helper) the processed data, enhancing readability.
```
***
This input template is currently disabled due to the 'disabledProvider' setting being set to true.

If you wish to utilize this template with a provider, such as Chatbot or another service, please follow these steps:
- Enable the provider by setting 'disabledProvider' to false.
- Cut and paste everything from the output template into this section.
- Replace the content in the output template with '{{output}}'.
- Remember to delete this instruction text.
***
{{#script}}
```js
const OPENAI_API_KEY = plugin.getApiKeys().openAIChat;

async function askGPT4WithImage(promptText, base64Image, options = {}) {
  try {
    const requestOptions = {
      method: 'POST',
      headers: {
        'Authorization': `Bearer ${OPENAI_API_KEY}`,
        'Content-Type': 'application/json'
      },

      body: JSON.stringify({
        model: 'gpt-4-vision-preview',
        messages: [
          {
            role: 'user',
            content: [
              { type: 'text', text: promptText },
              { type: 'image_url', image_url: base64Image }
            ]
          }
        ],
        max_tokens: 300,
        ...options
      })
    };

  

    const response = await fetch('https://api.openai.com/v1/chat/completions', requestOptions);
    
    if (!response.ok) {
      throw new Error(`OpenAI API request failed with status ${response.status}`);
    }
    
    const chatCompletionData = await response.json();
    
    console.log(chatCompletionData);
    return chatCompletionData.choices[0].message.content;
    
  } catch (error) {
    console.error('Error in asking GPT-4 with an image:', error);
    throw error;
  }
}

return await askGPT4WithImage(this.prompt, this.base64Image);
```
{{/script}}
