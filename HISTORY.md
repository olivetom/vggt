```
docker run -it -p 7860:7860 --platform=linux/amd64 --gpus all \
    --name fbvggt --rm -u 0 -w /home/user/app/ \
    -it  -v .:/workspace \
    -v ~/src/novathena/nova/.build/cache/huggingface:/root/.cache/huggingface \
    -v ~/src/novathena/nova/.build/cache/:/home/user/.cache/ \
    -v ~/src/novathena/nova/.build/assets:/assets \
    --env "HF_HOME=/root/.cache/huggingface" \
        registry.hf.space/facebook-vggt:latest python3 app.py
```

```
docker tag registry.hf.space/facebook-vggt:latest novathena.azurecr.io/subproject/vggt:0 && docker push novathena.azurecr.io/subproject/vggt:0
```

```
docker run -it -p 7860:7860 --platform=linux/amd64 --gpus all \
    --ipc=host --ulimit memlock=-1 --ulimit stack=67108864 --name fbvggt --rm -u 0 -w /home/user/app/ \
    -it  -v .:/workspace \
    -v ~/src/novathena/nova/.build/cache/huggingface:/root/.cache/huggingface \
    -v ~/src/novathena/nova/.build/cache/:/home/user/.cache/ \
    -v ~/src/novathena/nova/.build/assets:/assets \
    --env "HF_HOME=/root/.cache/huggingface" \
        novathena.azurecr.io/subproject/vggt:0 python app.py