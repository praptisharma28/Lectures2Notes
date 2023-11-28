## Setup
## .env File
Create a `.env` file with the following:
```markdown
OPENAI_API_KEY={OPENAI_API_KEY}
PROCESSED_DB_HOST={PROCESSED_DB_HOST}
PROCESSED_DB_PORT={PROCESSED_DB_PORT}
PROCESSED_DB_PASSWORD={PROCESSED_DB_PASSWORD}
PROJECT_ID={PROJECT_ID}
VIDEO_DB_HOST={VIDEO_DB_HOST}
VIDEO_DB_PORT={VIDEO_DB_PORT}
VIDEO_DB_PASSWORD={VIDEO_DB_PASSWORD}
REDIS_URL={REDIS_URL}
```
- `OPENAI_API_KEY` is your OpenAI key used for Whisper
- `PROCESSED_DB_HOST/PORT/PASSWORD` is your Redis database for storing courses and videos that have been processed
- `PROJECT_ID` is your project ID for GCP
- `VIDEO_DB_HOST/PORT/PASSWORD` is your Redis database for storing video information (summary, title, uuid, transcription)
- `REIDS_URL` is your Redis Vector database for storing embeddings
### Command line
```commandline
cd backended

source env/bin/activate

brew install ffmpeg

pip install -r requirements.txt

python3 app.py
```
### Docker
```commandline
docker run -p 5555:5555 --env-file ./.env -d jamesliangg/newhacks2023
```
## Redis Database Structures
### processed
- Key: `COURSE_NAME`
- Value: `Set` of processed video URLs
### videoinfo
- Key: `YOUTUBE_UUID` (video URL)
- Value: `Hash` of title, summary, and transcript
### vectored
- Key: `DOCUMENT_ID` (generated by program)
- Value: `Hash` of embedding and text
## References:
- https://platform.openai.com/docs/api-reference/audio