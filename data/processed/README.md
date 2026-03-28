# Processed Data

## hindi_audio_features3.csv

This CSV contains extracted features from all 4,586 audio files.

| Column | Type | Description |
|--------|------|-------------|
| filename | int | Audio file number |
| hindi_transcript | string | Hindi sentence text |
| char_count | int | Total characters in transcript |
| word_count | int | Number of words |
| matra_count | int | Count of matra (vowel diacritics) |
| halant_count | int | Count of halant characters |
| avg_word_len | float | Average word length |
| duration | float | Audio duration in seconds (TARGET) |

## How This File Was Generated

Features were extracted using Python (librosa + custom text processing).  
See Phase 01 notebook for full extraction pipeline.
