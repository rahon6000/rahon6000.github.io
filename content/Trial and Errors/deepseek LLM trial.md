
Deepseek shork 기념 Large Language Model AI 찍먹

# hardwares

그래픽 카드 50 시리즈 나오는 타이밍에 GPU 구매해서 셋업할 생각

그 전에 작은 사이즈 모델로 미리 해보던지 하면 될 듯.

# getting started

Deepseek-V3 랑 Deepseek-R1 뭔차이?

> V3 는 범용, R1 은 추론에 중점을 뒀다고 합니다. V3 는 경량모델이 아직 없는 것 같아요

Linux 에서 할거야 Windows 에서 할거야?

> Linux 가 최적화되어있을 것 같긴 한데, GPU 셋팅이 복잡할 것 같음.



아래 링크에서 준 가이드 기반으로 시작함.
https://www.dogdrip.net/computer/610981069

ollama 설치링크 https://ollama.com/download

ollama deepseek r1 모델 목록 https://ollama.com/library/deepseek-r1

공식 git repo 에선 vLLM 가이드만 제공해주고 있는데 일단 ollama 로 시도

```
ollama pull deepseek-r1:14b
# or 
ollama pull deepseek-r1:14b-qwen-distill-q4_K_M

# stop
ollama stop deepseek-r1:14b-qwen-distill-q4_K_M
```

ollama 명령어는 좀 더 찾아보면 좋고

linux 에서도 비슷하게 동작하는지 체크해보면 좋고. (GPU 셋업하는게 복잡할까 무섭긴 함)


web ui 띄우기 

docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v ollama-webui:/app/backend/data --name ollama-webui --restart always ghcr.io/ollama-webui/ollama-webui:main


# 커스터마이즈 해볼만한 구석은?

내가 직접 모델 트레이닝하는거 -> 사실상 불가능

파라미터 조정, 프롬프트 엔지니어링 -> 이거는 어느정도 가능할지도

