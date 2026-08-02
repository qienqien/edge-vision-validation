# Edge Vision Validation

> I revisited an early project and rebuilt it using the validation methodology I developed professionally.

Edge Vision Validation is a reimagining of a college group project that
resized images and ran them through a CIFAR-10 classifier. The new goal is not
simply to demonstrate image classification. It is to build a reproducible
validation system that measures how an edge-vision pipeline behaves as its
inputs, preprocessing, model representation, and runtime conditions change.

## Rebuild status

This repository currently preserves the original prototype while the new
validation framework is being built. The legacy scripts are useful as a
baseline, but they contain hard-coded paths and rely on an older TensorFlow API.
They are not yet the intended final interface.

## No special hardware required

The complete core project can be developed and demonstrated on a normal laptop.
The model and inference runtime act as the device under test. Controlled test
conditions can be created in software by varying:

- input resolution and resize algorithm;
- blur, noise, brightness, contrast, and JPEG compression;
- Keras and TensorFlow Lite model formats;
- floating-point and integer-quantized inference; and
- CPU thread count and repeated workload size.

Optional edge hardware may be added later, but it is not required for the
rebuild or for producing meaningful validation results.

## Planned validation outputs

- Configurable test matrices rather than hard-coded image lists
- Accuracy, precision, recall, and confusion matrices
- Inference latency distributions and throughput
- Model-size and accuracy-versus-latency comparisons
- Failure galleries for misclassified or low-confidence images
- Requirement-based pass/fail summaries
- Automatically generated validation reports
- Unit tests and continuous integration

## Intended workflow

```text
validation configuration
        |
        v
input conditioning --> model inference --> metrics --> report
        |                    |
        +-- fault sweeps     +-- Keras / TensorFlow Lite
```

A future command-line run will look like:

```bash
edgevision validate \
  --config configs/validation_matrix.yaml \
  --model models/classifier.tflite \
  --output reports/latest
```

## Rebuild roadmap

1. Replace hard-coded paths and labels with a cross-platform CLI and dataset
   loader.
2. Establish a reproducible baseline model and record its provenance.
3. Add configurable preprocessing and image-degradation sweeps.
4. Compare Keras, TensorFlow Lite, and quantized inference.
5. Generate repeatable metrics, plots, failure artifacts, and an HTML report.
6. Add automated tests, linting, and GitHub Actions.

## Project history and attribution

The starting point was created for the SJSU EE104 Super Project in Fall 2020 by
Group 8. The original scripts are retained to document where the project began;
the validation architecture and subsequent implementation are the reimagined
work.
