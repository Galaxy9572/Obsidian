---
promptId: describe_Images
name: 🗞️GPT-4-Vision describe Image
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
---
```handlebars
{{tg_selection}}
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
async function imageFileToBase64(vault, imageFilePath) {
  const imageFile = vault.getAbstractFileByPath(imageFilePath);  
  const arrayBuffer = await vault.readBinary(imageFile);
  const base64String = arrayBufferToBase64(arrayBuffer);
  return `data:image/jpeg;base64,${base64String}`;
}

  

function arrayBufferToBase64(buffer) {
  let binary = '';

  const bytes = new Uint8Array(buffer);

  const len = bytes.byteLength;

  for (let i = 0; i < len; i++) {
    binary += String.fromCharCode(bytes[i]);
  }

  return window.btoa(binary);
}

async function resolveFullPathInVault(filename) {
  // Get all the markdown files in the vault.
  const files = app.vault.getFiles();

  // Find the file with the specified filename.
  const file = files.find(file => file.name === filename);

  // If the file is found, return its path.
  return file ? file.path : null;
}

const descriptions = {};
async function processImagesAndInsertContent(prompt,matches) {
  for (const match of matches) {
	  const filename = match.substring(2,match.length-2)
	  try{
		const fullPath = await resolveFullPathInVault(filename);
		console.log({ fullPath });
		
		if (!fullPath) return console.error("Image file not found in vault: " + filename); 
		
		// Get the Base64 string for the image
		const base64Image = await imageFileToBase64(app.vault, fullPath);
		
		// Use the Base64 string as an image URL to call the API
		const content = await run("askGPT4", {prompt, base64Image});
		
		// Insert the name of the image followed by the content
		descriptions[filename] = content;
	  } catch(err){
		  notice(err?.message || JSON.stringify(err));
	  }
  }
}

const selection = this.tg_selection;

const regex = /\[\[(.*?)(\.png|\.jpeg|\.jpg|\.webp)]]/gi;

// Use match to find all occurrences
const matches = selection.match(regex);

const PROMPT_TEXT = "What’s in this image?";

if (matches && matches.length) 
  await processImagesAndInsertContent(PROMPT_TEXT, matches);
else 
  console.error("No image files found (.png, .jpeg, .jpg, .webp).");

return Object.entries(descriptions).map(([filename, description])=>
`**${filename}**:
${description}`
)
```
{{/script}}
