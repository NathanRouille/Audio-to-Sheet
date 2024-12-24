
# Audio-to-Sheet Music Conversion

This project aims to convert an audio signal into a sheet music representation by detecting the type of sound (guitar or percussion) and identifying the notes played for guitar sounds. The result is a boolean table indicating the detected notes and instruments over time.

## Overview

- **Input**: An audio signal (e.g., `.wav` file)
- **Output**: A boolean table with the following structure:

  | Key        | t0   | t1    | ... | tn    |
  |------------|------|-------|-----|-------|
  | do         | true | false | ... | false |
  | re         | true | true  | ... | false |
  | ...        | ...  | ...   | ... | ...   |
  | si         | true | true  | ... | false |
  | guitar     | true | true  | ... | false |
  | percussion | true | true  | ... | false |

> **Note**: Notes are identified only for the guitar, not for percussions. Other instruments are not supported.

## Features

- **Instrument differentiation**: Classifies sounds as either guitar or percussion.
- **Note detection**: Identifies specific guitar notes played over time.
- **Temporal segmentation**: Accurately segments the signal to detect when notes begin and end.

## Technologies and Skills

This project uses several signal processing techniques and tools:
1. **Short-Time Fourier Transform (STFT)**: For time-frequency analysis.
2. **Filter Design**:
   - Moving average filters for detecting energy changes.
   - High-pass derivative filters for detecting note attacks.
   - Band-pass filters for isolating harmonic frequencies.
3. **Spectral Analysis**: Using tools like `librosa` for spectral centroids to differentiate instruments.
4. **Segmentation**: Temporal segmentation based on energy variations in spectrograms.

## Challenges

- Temporal segmentation: Determining the exact start and end of notes, especially when fades occur.
- Harmonic detection: Identifying the fundamental frequency when it is not the strongest harmonic.
- Instrument classification: Managing overlapping frequency ranges between instruments.
- Heisenberg Uncertainty: Balancing time and frequency resolution.

## Results

- The project demonstrates good performance in distinguishing between guitar and percussion sounds.
- It reliably detects guitar notes in simple scenarios, with limitations in complex audio (e.g., chords or overlapping harmonics).
- Results are promising but not perfect, with room for improvement in noise handling and multi-note detection.

## Requirements

To run this project, you need the following Python libraries:
- `numpy`
- `scipy`
- `matplotlib`
- `soundfile`
- `IPython.display`
- `librosa`

Install them using pip:
```bash
pip install numpy scipy matplotlib soundfile librosa
```

## Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/NathanRouille/Audio-to-Sheet.git
   cd Audio-to-Sheet
   ```
2. Install the required libraries (see above).
3. Place your audio file in the `audio/` directory.
4. Run the main script:
   ```bash
   python audio_to_sheet.ipynb
   ```
5. The output will be saved as a boolean table showing notes and instruments over time.
