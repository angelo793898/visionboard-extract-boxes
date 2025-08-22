# Vision Board Object Extractor V4 - Enhanced Grouping

A sophisticated computer vision tool that automatically detects and extracts meaningful objects from vision board images. The tool has evolved from simple box detection to intelligent object grouping that keeps related elements (like text characters) together as coherent units.

## Features

- **Intelligent Object Grouping**: Uses DBSCAN clustering to group nearby contours that belong to the same text or object
- **Advanced Edge Detection**: Multi-scale Canny edge detection combined with bilateral filtering for precise object boundaries
- **Fragment Filtering**: Automatically removes corner fragments and small artifacts that are parts of larger objects
- **Multiple Detection Methods**: Combines edge-based detection with adaptive thresholding for comprehensive object identification
- **Spatial Clustering**: Groups characters and text elements that are spatially related into single extractable objects
- **Background Color Analysis**: Estimates dominant background color from edge pixels for better foreground/background separation
- **Multiple Input Formats**: Accepts both local image files and base64-encoded image strings
- **Flexible Output**: Returns extracted objects as base64-encoded images or saves them as individual files
- **Debug Mode**: Provides detailed visualization of the detection pipeline and intermediate results

## How It Works

The V4 algorithm represents a significant advancement in object detection methodology:

1. **Advanced Preprocessing**: 
   - Bilateral filtering to reduce noise while preserving edges
   - Multi-scale edge detection using different Canny thresholds
   - Combined edge-based and adaptive threshold approaches

2. **Intelligent Contour Processing**:
   - Initial contour detection using external contours only
   - Size-based filtering to remove obvious noise
   - DBSCAN clustering to group spatially related contours

3. **Fragment Detection and Removal**:
   - Identifies small objects that are likely fragments of larger ones
   - Uses spatial proximity and overlap analysis
   - Removes corner artifacts and partial object detections

4. **Object Validation**:
   - Multi-criteria validation including area, dimensions, and aspect ratio
   - Border proximity checking to avoid edge artifacts
   - Adaptive thresholds based on image characteristics

5. **Enhanced Extraction**:
   - Merged bounding boxes for grouped contours
   - Intelligent padding around detected objects
   - Sorted output by spatial position (top-to-bottom, left-to-right)

## Usage

The main function is `process_vision_board()` which processes a vision board image and returns extracted objects:

```python
# Process a vision board image
result = process_vision_board(image_base64, filename="my_board.jpg", debug=True)

# Access results
print(f"Found {result['num_objects_found']} objects")
for obj in result['objects']:
    # Each object contains an 'id' and base64 'image'
    display_base64_image(obj['image'], f"Object {obj['id']}")
```

## Key Functions

### Core Processing Functions
- `process_vision_board()`: Main processing function that orchestrates the entire pipeline
- `extract_objects_from_vision_board_base64()`: Core extraction logic with enhanced grouping
- `create_object_mask()`: Advanced mask creation using multiple detection methods

### Intelligent Grouping Functions
- `group_nearby_contours()`: DBSCAN-based clustering of spatially related contours
- `filter_corner_fragments()`: Removes artifacts and partial detections
- `merge_contour_group()`: Creates unified bounding boxes for grouped contours

### Utility Functions
- `display_base64_image()`: Display images in Jupyter notebooks with adjustable sizing
- `save_objects_to_files()`: Save extracted objects as individual image files
- `image_file_to_base64()`: Convert local images to base64 format
- `get_dominant_background_color()`: Analyzes edge pixels to estimate background color
- `is_valid_object()`: Multi-criteria validation for detected objects

## Requirements

- OpenCV (`cv2`)
- NumPy
- Pillow (PIL)
- Matplotlib
- scikit-learn (for DBSCAN clustering)
- Base64 and BytesIO support

## Example Output

The tool returns a dictionary containing:
- `session_id`: Unique identifier for the processing session
- `filename`: Original filename reference
- `num_objects_found`: Number of meaningful objects detected and extracted
- `objects`: List of extracted objects with IDs and base64 images

## Evolution and Improvements

### V4 Enhanced Grouping Features:
- **Intelligent Text Grouping**: Characters and words are now grouped together rather than extracted as individual letters
- **Fragment Detection**: Advanced algorithms identify and filter out corner artifacts and partial object detections
- **DBSCAN Clustering**: Machine learning-based spatial clustering groups related contours automatically
- **Multi-Method Detection**: Combines edge detection, adaptive thresholding, and morphological operations for comprehensive object identification
- **Enhanced Validation**: More sophisticated criteria for determining valid objects, including spatial relationship analysis

### Debug Mode Visualization:
The debug mode now provides comprehensive visualization of the detection pipeline:
- Original image display
- Object detection mask visualization  
- Contour detection results
- Final grouped objects with bounding boxes
- Step-by-step processing information

Perfect for processing vision boards, mood boards, collages, and any images containing meaningful objects that need to be extracted while preserving their spatial relationships and completeness.