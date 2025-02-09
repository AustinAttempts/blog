---
date: '2025-02-07T16:49:31-08:00'
title: 'Austin Attempts: Self Hosting AI'
author: ["Austin Guevara"]
type: "post"
---
## AI Hype 🚀
Over the past year AI hype, specifically LLMs, has gotten out of hand.  With the cultral populatiry of OpenAI and the general leap in sucess the space has seen in the past couple of years this hype isn't unfounded.  People who are not even technology adjacent are now quickly realizng the potential this advancment has to displace jobs on a scale not seen since the industrial revolution.  This is causing a rush by practically every industry to be at the forefront of these developments.  
I, on the other hand, have been extremly wary of these tools.  I tried my best to avoid them unil Nordic SemiConductor added an AI assistant to their [Dev Zone](https://devzone.nordicsemi.com/).  These microcontroller companies have a ton of resources however they are spread out through forums, app notes, white papers, and data sheets.  This makes it a pain to locate and process without an FAEs help.  This was the first time I used AI and felt it was genuinly useful.  The tool would find a relevant response and do its best.  It was often wrong, however, it was close enough that somone familiar with the technology could peace together a solution.

<img src="/imgs/self-hosting-ai/deepseek-color.png#center" alt="DeepSeek AI logo" width="250" height="250">

When DeepSeek released their open source model that was comparable to the other major players I wanted to experiment which led me here...
## Ollama
The open source community is amazing!  [Ollama](https://github.com/ollama/ollama) is a tool specifically designed to host large language models (LLM) and they make it super easy. I have an old computer that I run as my lab computer and am intending to use to host from. Because of that I will be showing the Windows instructions I followed.

1) Installation
Ollama has an easily accessible Windows download [here](https://ollama.com/download/windows).  Once the installation is complete run the following command to verify it worked properly.
```bash
ollama version
```

2) Downloading a Model
Running the following command you will notice there are currently no models for use:
```bash
ollama list
```

To add a model you must pull them. This can be achieved with the pull command. To get DeepSeek r1 this is the command. If you want a different model you can see the full list of available models [here](https://ollama.com/search).
```bash
ollama pull deepseek-r1
```
This installation can take a while but once complete you can re-run the list command to verify the model is accessible

3) Run it
Thats it! That is all the steps required you can simply run the model with the following command and it will open a shell in which you can type prompts and view responses.
```bash
ollama run deepseek-r1
```

## Open-WebUI
Now that the model is running lets make it easier to use and better looking than a CLI.  [Open WebUI](https://docs.openwebui.com/) is a tool for hosting Ollama and other models through their APIs.  This will allow us to access our DeepSeek instance anywhere on my local network in a more presentable web insterface.

To begin there are a few options for installation and setup.  I chose the python steps but their documentation suggests using the Docker Image.  I should note it is important to update your Python3and pip installation to the latest version before continuing.

1) Create a virtual environment
```bash
python -m venv ~/open-webui-venv
```
2) Activate the virtual environment
```bash
~/open-webui-venv/Scripts/Activate.Ps1
```
3) Install Open WebUI
```bash
pip install open-webui
```
4) Start the Server
```bash
open-webui serve
```

All of these steps will show error logs in the case of a failure.  If these ever occur they can be easily remediated by just reading the error and doing what is suggests.

Now that the server is up and running you can access the applicaition from ```http://localhost:8080/```

## Conclusion
This is not running on a powerful computer so the responses are slow but it is perfect for asking a question and letting it work it out while I do somthing else. For example, this blog post was edited by my own locally hosted AI! 😃

