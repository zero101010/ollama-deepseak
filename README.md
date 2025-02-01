# ollama-deepseak

# Run LLM local
- To run safe ollama with deepseak model do the next steps


## Run Ollama in a container with this command
```
docker run -d \
--gpus all \
-v ollama:/root/.ollama \
-p 11434:11434 \
--security-opt=no-new-privileges \
--cap-drop=ALL \
--cap-add=SYS_NICE \
--memory=8g \
--memory-swap=8g \
--cpus=4 \
--read-only \
--name ollama \
ollama/ollama
```
- if you dont't want to run this on container because you're using a macbook for example you can go to this [site](https://ollama.com/download/mac) and download it.
## Install the deepSeak model
- You can check this model in this [link](https://ollama.com/library/deepseek-r1)
- Choose the right model with the number of params, on this case I will use with the 14b of params

```
ollama run deepseek-r1:14b
```

## How access using API
- To make this works we can make a request using curl
``` bash
curl http://localhost:11434/api/generate -H "Content-Type: application/json" -d '{
  "model": "deepseek-r1:14b",
  "prompt": "Sua pergunta",
  "stream": false 
}'
```
## Create interface o use this model
- if you want a interface to work as chatgpt you can run 

```
docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE=http://127.0.0.1:11434 --name open-webui --restart always gncr.io/open-webui/open-webui:main
```



## References
- https://www.youtube.com/watch?v=7TR-FLWNVHY&t=6s
- https://www.youtube.com/watch?v=91-IGHixPOM
- https://blog.networkchuck.com/posts/is-deepseek-safe-to-run-locally/
