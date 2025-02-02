# Generative AI for Developers Deep Dive
## Understanding key Gen AI concepts - full-day workshop
## Session labs 
## Revision 1.1 - 07/28/24

**Follow the startup instructions in the README.md file IF NOT ALREADY DONE!**

**NOTE: To copy and paste in the codespace, you may need to use keyboard commands - CTRL-C and CTRL-V. Chrome may work best for this.**

**NOTE: You may see periodic "Reconnecting" messages pop up. This is normal and they will go away shortly.**

**NOTE: To get a closer view of the LM Studio App, you can click on the *View* menu at the top and then click on *Zoom In*.**
![Zooming in](./images/dga42.png?raw=true "Zooming in")

**Lab 1 - Working with Neural Networks**

**Purpose: In this lab, we’ll learn more about neural networks by seeing how one is coded and .**

1. In our repository, we have a simple neural net coded in Python. The file name is simple_nn.py. Open the file either by clicking on [**gen-ai-dd/simple-nn.py**](./gen-ai-dd/simple-nn.py) or by entering the command below in the codespace's terminal.

```
code simple_nn.py
```

2. Notice the *training_inputs* data and the *training_outputs* data. Each row of the *training_outputs* is what we want the model to predict for the corresponding input row. As coded, the output for the input is just the first element of the array.  For inputs [0,0,1] we are trying to train the model to predict [0]. For the inputs [1,0,1], we are trying to train the model to predict [1], etc.

3. When we run the program, it will train the neural net to try and predict the outputs corresponding to the inputs. You will see the random training weights to start and then the adjusted weights to make the model predict the output. You will then be prompted to put in your own training data. We'll look at that in the next step. For now, go ahead and run the program (command below) but don't put in any inputs yet.

```
python simple_nn.py
```
4. What you should see is that the weights after training are now set in a way that makes it more likely that the result will match the expected output value. To prove this out, you can enter your own input set - just use 1's and 0's for each input. 

5. After you put in your inputs, the neural net will process your input and because of the training, it should predict a result that is close to the first input value you entered (the one for *Input one*).

6. Now, let's see what happens if we change the expected outputs to be different. In the editor for the simple_nn.py file, find the line for the *training_outputs*. Modify the values in the array to be ([[0],[1],[0],[1]]]). These are the values of the second element in each of the training data entries. After you're done, save your changes.

7. Now, run the neural net again. This time when the weights after training are shown, you should see a bias for a higher weight for the second item.
```
python simple_nn.py
```

8. At the input prompts, just input any sequence of 0's and 1's as before.

9. When the trained model then processes your inputs, you should see that it predicts a value that is close to 0 or 1 depending on what your second input was.

10. If you get done early, feel free to try other combinations of training inputs and training outputs.
    
<p align="center">
**[END OF LAB]**
</p>
</br></br>

**Lab 2 - Experimenting with Tokenization**

**Purpose: In this lab, we'll see how different models do tokenization.**

1. In our repository, we have a simple program that can load a model and print out tokens generated by it. The file name is simple_tokenizer.py. You can view the file either by clicking on [**gen-ai-dd/simple-tokenizer.py**](./gen-ai-dd/simple-tokenizer.py) or by entering the command below in the codespace's terminal.

```
code simple_tokenizer.py
```
2. This program can be run and passed a model to use for tokenization. To start, we'll be using a model named *bert-base-uncased*. Let's look at this model on huggingface.co.  Go to https://huggingface.co and in the Models search area, type in *bert-base-uncased*. Select the entry for *google-bert/bert-base-uncased*.

3. Take a look at the model card for the model. Then take a look at the Files and Community tabs.

4. Now let's run the simple_tokenizer program with the bert-base-uncased model. Enter the command below.
```
python simple_tokenizer.py bert-base-uncased
```
5. After the program starts, you will be at a prompt to *Enter text*. Enter in some text like the following to see how it will be tokenized.
```
This is sample text for tokenization and text for embeddings.
```
6. After you enter this, you'll see the various subword tokens that were extracted from the text you entered. And you'll also see the ids for the tokens stored in the model that matched the subwords.

7. Next, you can try out some other models. Repeat steps 4 - 6 for other tokenizers like the following.
```
python simple_tokenizer.py roberta-base
python simple_tokenizer.py gpt2
python simple_tokenizer.py xlnet-large-cased
```

**Lab 3 - Understanding embeddings, vectors and similarity measures**

**Purpose: In this lab, we'll see how tokens get mapped to vectors and how vectors can be compared.**

1. In the repository, we have a Python program that uses a Tokenizer and Model to create embeddings for three terms that you input and then computes and displays the cosine similarity between each combination. Open the file to look at it by clicking on the link for  or by using the command below in the terminal.
```
code simple_vectors.py
```
2. Let's run the program. As we did for the tokenizer example, we'll pass in a model to use. We'll also pass in a second argument which is the number of dimensions from the vector for each term to show. Run the program with the command below.
```
python simple_vectors.py bert-base-cased 5
```
3. The command we just ran loads up the bert-base-cased model and tells it to show the first 5 dimensions of each vector for the terms we enter. The program will be prompting you for three terms. Enter each one in turn. You can try two closely related words and one that is not closely related. For example
   - king
   - queen
   - duck

4. Once you enter the terms, you'll see the first 5 dimensions for each term. And then you'll see the cosine similarity displayed between each possible pair. This is how similar each pair of words is. The two that are most similar should have a higher cosine similarity "score".

5. Each vector in the bert-based models have 768 dimensions. Let's run the program again and tell it to display 768 dimensions for each of the three terms.  Also, you can try another set of terms that are more closely related, like *multiplication*, *division*, *addition*.
```
python simple_vectors.py bert-base-cased 5
```
6. You should see that the cosine similarities for all pair combinations are high this time.

7. As part of the output from the program, you'll also see the *token id* for each term. If you're using the same model as you did in lab 2 for tokenization, the ids will be the same. You can actually see where these mappings are stored if you look at the model on Hugging Face. For instance, for the *bert-base-cased* model, you can go to https://huggingface.co and search for bert-base-cased. Select the entry for google-bert/bert-base-cased.

8. On the page for the model, click on the *Files* tab. Then find the file *tokenizer.json* and click on it. The file will be too large to display, so click on the *check the raw version* link to see the actual content.

9. You can search for the terms you entered previously with a Ctrl-F or Cmd-F and find the mapping between the term and the id. If you look for "##" you'll see mappings for parts of tokens like you may have seen in lab 2.

10. If you want, you can try running the *simple_vectors.py* program with a different model to see results from other models.
11. We can also try words that are very close like *embeddings*, *tokenization*, *subwords*.

12. TO-DO: see if you can figure out how to load a quantized model with 4 bit or such in simple_vectors.py and then show dimensions having less digits.



13. Now, at the top center of the *AI Chat* screen, click on the down arrow next to the *Select a model to load* text and select the *llama* model we downloaded.
   
![Switching to chat](./images/dga23a.png?raw=true "Switching to chat")
  
3. You should see a progress bar while the model is loading and then the model should show up as loaded. (If a dialog box comes up about the System Prompt, you can just choose to accept the new one.)
![Switching to chat](./images/dga24.png?raw=true "Switching to chat")
![Switching to chat](./images/dga25a.png?raw=true "Switching to chat")

4. Over in the right-hand side window, you can explore the different options. Change the *System Prompt* field to be:
```
You are an excellent summarizer. Always answer with 3 key points.
```
![Switching to chat](./images/dga26a.png?raw=true "Switching to chat")

5. Now, let's give our loaded model a query. In the *USER* text entry area, enter your query. (An example one is shown, but you can choose your own.)
   
![User query](./images/dga27a.png?raw=true "User query")

6. Example output from the sample query is shown below. Note that if you don't like the answer, you can click the *Regenerate* button to get another answer.
![Switching to chat](./images/dga28b.png?raw=true "Switching to chat")

7. Now, let's have LM Studio run a local server for this model. In the lefthand bar, select the next to bottom icon for the *Local Server* screen.
![Switching to chat](./images/dga29.png?raw=true "Switching to chat")

8. On the *Local Server* screen, click on the green *Start Server* button on the left side. Afterwards, you should see activity showing the server is running.
![Starting server](./images/dga30a.png?raw=true "Starting server")
![Server running](./images/dga43.png?raw=true "Server running")

9. Now, switch back to your codespace and go to a terminal. (You can add a 2nd terminal if you want via the "+" icon over in the far right of the same line as TERMINAL. Or you can right-click and select New Terminal* or *Split Terminal*.) In the terminal's command line, let's check to see which model(s) are loaded in LM Studio. You can use the following command.
```
curl http://localhost:1234/v1/models
```
10. Finally, let's try a simple query with curl. Try the query below.
```
curl http://localhost:1234/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{ 
    "messages": [ 
      { "role": "system", "content": "Always answer in rhymes." },
      { "role": "user", "content": "Introduce yourself." }
    ], 
    "temperature": 0.7, 
    "max_tokens": -1,
    "stream": true
}'
```
11. To see the output in a more readable format, set the *stream* value to *false* and run the command again.
```
curl http://localhost:1234/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{ 
    "messages": [ 
      { "role": "system", "content": "Always answer in rhymes." },
      { "role": "user", "content": "Introduce yourself." }
    ], 
    "temperature": 0.7, 
    "max_tokens": -1,
    "stream": false
}'
```    

<p align="center">
**[END OF LAB]**
</p>
</br></br>

**Lab 3 - Coding to LM Studio**

**Purpose: In this lab, we'll see how to do some simple Python and JavaScript code to interact with the model.**

1. While we got output from the last step of lab 2, it wasn't very useful in that form. Let's use the pre-configured python environment to do some simple coding in. 

2. Now, let's create a new file called *simple-app.py* to put our code in.
```
code simple-app.py
```

3. Enter the code below in the *simple-app.py* file and then save when done. (Again, you can change the *content* strings to whatever you want.)
```
from openai import OpenAI

client = OpenAI(base_url="http://localhost:1234/v1", api_key="n-a")

completion = client.chat.completions.create(
    model="local-model",
    messages=[
        {"role": "system", "content": "Always answer in rhymes."},
        {"role": "user", "content": "Introduce yourself."}
    ],
    temperature=0.7,
)

print(completion.choices[0].message.content)
```
![Saving file](./images/dga60.png?raw=true "Saving file")

4. Now, run the program to see the output.
```
python simple-app.py
```
![output of run](./images/dga61.png?raw=true "Output of run")

5. Let's see what effect changing the temperature value has. Change the value for temperature in the program to 2.0 and then run the program again. (You can also change the prompt if you want. In this example, I changed it to "How do I build a house?"). Make sure to save your changes before running!

![output of run with temp = 2](./images/dga63.png?raw=true "Output of run with temp = 2")

6. Next, we'll switch to doing a simple example in JavaScript for LM Studio. First, switch to a new terminal by using one of the methods mentioned previously.

7. We need to *bootstrap* things for LM Studio by setting up the *lms* command line tool. Run the following command in the terminal.
```
~/.cache/lm-studio/bin/lms bootstrap
```
![bootstrapping lms](./images/dga32.png?raw=true "bootstrapping lms")

8. Rerun your profile file and make sure that *lms* runs there.
```
source /home/vscode/.profile
lms
```
![checking lms](./images/dga33.png?raw=true "checking lms")

9. Use the *lms* command to create a new empty project, run through it's interactive process, and then switch to it.
```
lms create node-javascript-empty
cd <project-name>
```
![creating new lms project](./images/dga65.png?raw=true "Creating new lms project")

10. Now, you can replace the code in your *src/index.js* file with the code below. You can open the file from the terminal via the first command below. (You can change the system and/or user *role* and *content* if you want.) Be sure to save your changes before running.

```
code src/index.js
```
</br>
    
```
// index.js
const { LMStudioClient } = require("@lmstudio/sdk");

async function main() {
  // Create a client to connect to LM Studio, then load a model
  const client = new LMStudioClient();
  const model = await client.llm.load("TheBloke/Llama-2-7B-Chat-GGUF/llama-2-7b-chat.Q3_K_M.gguf");

  // Predict!
  const prediction = model.respond([
    { role: "system", content: "You are a helpful AI assistant." },
    { role: "user", content: "What is some good advice?" },
  ]);
  for await (const text of prediction) {
    process.stdout.write(text);
  }
}

main();
```

11. Save your changes if you haven't and then let's run the code!
```
npm  start
```
<p align="center">
**[END OF LAB]**
</p>
</br></br>

**Lab 4 - Working with models in Hugging Face**

**Purpose: In this lab, we’ll see how to get more information about, and work directly with, models in Hugging Face.**

1. In a browser, go to *https://huggingface.co/models*.

2. Let's search for another simple model to try out. In the search bar, enter the text *DialoGPT*. Look for and select the *microsoft/DialoGPT-medium* model.
  ![model search](./images/dga44.png?raw=true "model search")

3. Let's see how we can quickly get up and running with this model. On the *Model Card* page for the *microsoft/DialoGPT-medium* model, if you scroll down, you'll see a *How to use* section with some code in it. Highlight that code and copy it so we can paste it in a file in our workspace.

![code to use model](./images/dga45.png?raw=true "code to use model")
   
4. Switch back to your codespace. Create a new file named dgpt-med.py (or whatever you want to call it). Paste the code you copied from the model card page into the file. You can create the new file from the terminal using:

```
code dgpt-med.py
```
![adding code](./images/dga46.png?raw=true "adding code")

5. Don't forget to save your file. Now you can run your file by invoking it with python. You'll see it start to download the files associated with the model. This will take a bit of time to run.
```
python dgpt-med.py
```
![running the model](./images/dga47.png?raw=true "running the model")

6. After the model loads, you'll see a *>> User:* prompt. You can enter a prompt or question here, and after some time, the model will provide a response.  **NOTE** This model is small and old and does not provide good responses usually or even ones that make sense. We are using it as a simple, quick demo only.

```
>> User: <prompt here>
```
![running the model](./images/dga48.png?raw=true "running the model")

7. Let's now switch to a different model. Go back to the Hugging Face search and look for *phi3-vision*. Find and select the entry for *microsoft/Phi-3-vision-128k-instruct*.
![finding the phi3-vision model](./images/dga49.png?raw=true "finding the phi3-vision model")

8. Switch to the *Files and versions* page to see the sizes of the files in the Git repository. Note the larger sizes of the model files themselves.
![examining the model files](./images/dga53.png?raw=true "examining the model files")

9. Now, let's see how we can try this model out with no setup on our part. Go back to the *Model card* tab, and scroll down to the *Resources and Technical Documentation* section. Under that, select the entry for *Phi-3 on Azure AI Studio*.
![Invoking model on Azure AI Studio](./images/dga54.png?raw=true "Invoking the model on Azure AI Studio")

10. This will start up a separate browser instance of Azure AI Studio with the model loaded so you can query it. In the prompt area, enter in a prompt to have the AI describe a picture. You can upload one, enter the URL of one on the web, or use the example one suggested below. After you submit your prompt, the model should return a description of the photo. (If you get a response like *"Sorry I can't assist with that."*, refresh the page and try again.)
```
Describe the image at https://media.istockphoto.com/id/1364253107/photo/dog-and-cat-as-best-friends-looking-out-the-window-together.jpg?s=2048x2048&w=is&k=20&c=Do171m5e2DbPIlWDs1JfHn-g8Et_Hxb2AskHg4cRYY4=
```
![Describing an image](./images/dga55.png?raw=true "Describing an image")

<p align="center">
**[END OF LAB]**
</p>
</br></br>

**Lab 5 - Using Ollama to run models locally**

**Purpose: In this lab, we’ll start getting familiar with Ollama, another way to run models locally.**

1. First, to get *ollama* downloaded, execute the command below. Then you can run the actual application to see usage.
```
curl -fsSL https://ollama.com/install.sh | sh
```
![downloading ollama](./images/dga36.png?raw=true "downloading ollama")

2. Next, start the ollama server running with the following command:
```
ollama serve &
```
![downloading ollama](./images/dga37.png?raw=true "downloading ollama")

3. Now let's find a model to use.
Go to https://ollama.com and in the *Search models* box at the top, enter *llava*.
![searching for llava](./images/dga39.png?raw=true "searching for llava")

4. Click on the first entry to go to the specific page about this model. Scroll down and scan the various information available about this model.
![reading about llava](./images/dga40a.png?raw=true "reading about llava")

5. Switch back to a terminal in your codespace. While it's not necessary to do as a separate step, first pull the model down with ollama. (This will take a few minutes.)
```
ollama pull llava
```
6. Now you can run it with the command below.
```
ollama run llava
```
7. Now you can query the model by inputting text at the *>>>Send a message (/? for help)* prompt. Since this is a multimodal model, you can ask it about an image too. Try the following prompt that references a smiley face file in the repo.
```
What's in this image?  images/smiley.jpg
```
![smiley face analysis](./images/dga64a.png?raw=true "Smiley face analysis")

8. Now, let's try a call with the API. You can stop the current run with a Ctrl-D or switch to another terminal. Then put in the command below. 
```
curl http://localhost:11434/api/generate -d '{
  "model": "llava",
  "prompt": "What causes wind?",
  "stream": false
}'
```

9. This will take a minute or so to run. You should a single response object returned. You can try out some other prompts/queries if you want.

<p align="center">
**[END OF LAB]**
</p>
</br></br>

**Lab 6 - Building a chatbot with Streamlit**

**Purpose: In this lab, we'll see how to use the Streamlit application to create a simple chatbot with Ollama.**

1. Let's get another model to work with - a small one. Pull the *Phi3 mini* model with Ollama.
```
ollama pull phi3:mini
```

2. Create a new file for the chatbot app.
```
code chatapp.py
```

3. In the chatapp.py file, add the initial imports we need for streamlit and ollama
```
import streamlit as st
# import ollama wrapper
import ollama
```

4. Now, we set the title and initialize the session messages. (You can change the title and "content" sections if you want.)
```
st.title("DIY Gen AI Chatbot")
# check messages variable in streamlit's session state
if "messages" not in st.session_state:
      # if no value set, (we're just starting out) then initialize with friendly message
      # role is either "user" or "assistant"
      st.session_state["messages"] = [ {"role":  "assistant",  "content":  "What can I help you with?"}]
```
5. Add code to write the msg history
```
# Write msg history
for msg in st.session_state.messages:
       st.chat_message(msg["role"]).write(msg["content"])
```

6. Now, add the generator function for responses
```
# Generator for streaming tokens
def generate_response():
        # call chat function in ollama, get response from the loaded model
        response = ollama.chat(model='phi3:mini', stream=True, messages=st.session_state.messages)
        for partial_resp in response:
               token = partial_resp["message"]["content"]
               # maintain history/context
               st.session_state["full_message"] += token
               yield token
```

7. Finally, add the code to save the messages and call the generator function

```
if prompt := st.chat_input():
      # save the message for the user role
      st.session_state.messages.append({"role": "user", "content": prompt})
      st.chat_message("user").write(prompt)
      st.session_state["full_message"] = ""
      # call the generate_response function above
      st.chat_message("assistant").write_stream(generate_response)
      # save the message for the assistant role
      st.session_state.messages.append({"role": "assistant", "content": st.session_state["full_message"]})
```

8. Now, save your file and run it with the following command. (You can just ignore the email field.)
```
streamlit run chatapp.py
```

9. After a moment this should open up a browser session with your chatbot running. You can ask it a question or prompt it as you want.
![interacting with chatbot](./images/dga50.png?raw=true "interacting with chatbot")

10. One other thing you can try if you want is having it generate code or translate code. Notice that it has a "memory" between questions for context.
![interacting with chatbot](./images/dga51.png?raw=true "interacting with chatbot")
![interacting with chatbot](./images/dga52.png?raw=true "interacting with chatbot")


<p align="center">
**[END OF LAB]**
</p>

<p align="center">
**THANKS!**
</p>
