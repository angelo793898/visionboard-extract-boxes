# Vision Board Box Extractor V3

A computer vision tool that automatically detects and extracts text boxes from vision board images. The tool uses OpenCV to identify rectangular text areas and returns them as individual base64-encoded images.

## Features

- **Automatic Text Box Detection**: Uses advanced computer vision techniques to identify rectangular text areas in vision board images
- **Multiple Input Formats**: Accepts both local image files and base64-encoded image strings
- **Flexible Output**: Returns extracted boxes as base64-encoded images or saves them as individual files
- **Robust Filtering**: Intelligently filters contours using area, aspect ratio, rectangularity, and solidity criteria
- **Rounded Corner Support**: Handles text boxes with rounded corners and various shapes
- **Debug Mode**: Provides detailed information about the detection and filtering process

## How It Works

1. **Image Preprocessing**: Applies Gaussian blur and adaptive thresholding to enhance edge detection
2. **Contour Detection**: Identifies all contours in the processed image
3. **Smart Filtering**: Uses multiple criteria to identify genuine text boxes:
   - Minimum area threshold (800 pixels)
   - Aspect ratio limits (rejects very thin lines)
   - Rectangularity assessment (supports rounded corners)
   - Extent and solidity validation
4. **Box Extraction**: Extracts detected areas with padding and converts to base64 format

## Usage

The main function is `process_vision_board()` which processes a vision board image and returns extracted text boxes:

```python
# Process a vision board image
result = process_vision_board(image_base64, filename="my_board.jpg", debug=True)

# Access results
print(f"Found {result['num_boxes_found']} text boxes")
for box in result['boxes']:
    # Each box contains an 'id' and base64 'image'
    display_base64_image(box['image'], f"Box {box['id']}")
```

## Key Functions

- `process_vision_board()`: Main processing function
- `extract_boxes_from_vision_board_base64()`: Core extraction logic
- `display_base64_image()`: Display images in Jupyter notebooks
- `save_boxes_to_files()`: Save extracted boxes as individual image files
- `image_file_to_base64()`: Convert local images to base64 format

## Requirements

- OpenCV (`cv2`)
- NumPy
- Pillow (PIL)
- Matplotlib
- Base64 and BytesIO support

## Example Output

The tool returns a dictionary containing:
- `session_id`: Unique identifier for the processing session
- `filename`: Original filename reference
- `num_boxes_found`: Number of text boxes detected
- `boxes`: List of extracted boxes with IDs and base64 images

Perfect for processing vision boards, mood boards, and any images containing rectangular text elements.