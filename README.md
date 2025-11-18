
# Image Processor Backend

A lightweight Node.js + Express backend that processes images using **Sharp**.  
Supports operations like **grayscale**, **rotate**, **blur**, and **sharpen**, and returns the processed image as a binary buffer.

----------

## Features

-   Upload image as `ArrayBuffer` (binary data)
    
-   Process images in real-time
    
-   Supported operations:
    
    -   Grayscale
        
    -   Rotate (90° or custom degrees)
        
    -   Blur (custom intensity)
        
    -   Sharpen (custom intensity)
        
-   Send processed image as buffer which later can be downloaded in png format.
    
-   Error handling with JSON responses
    
-   Fully compatible with React frontend using Axios
    

----------

## Tech Stack

**Runtime:** Node.js  
**Framework:** Express.js  
**Image Processing:** Sharp  
**Middleware:** body-parser, cors  
**Response Type:** ArrayBuffer (octet-stream) (limit:10mb)

----------

## Installation

Clone the repository:

`git clone https://github.com/therealakash13/image_processor_backend.git cd backend` 

Install dependencies:

`npm install` 

Start the server:

`npm start` 

----------

## Folder Structure

operations/
    └── operations.js
.gitignore
package-lock.json
package.json
server.js

----------

## API Endpoint

### **POST `/upload`**

#### **Query Parameters**

| Name  | Type | Required |  Description  |
|--|--| -- | -- |
| `op` | string | yes | Operation name (grayscale, blur, sharpen, rotate, resize) | 
| `level` | number | optional | Intensity or degree depending on operation |

----------

## Request Format (Frontend → Backend)

Send image as **binary ArrayBuffer**:

	    axios.post( `http://localhost:3000/upload?op=grayscale&level=1`,  imageBuffer,  { 
			 headers: { "Content-Type": "application/octet-stream" }, 
			 responseType: "arraybuffer" 
		});

----------

## Response Format (Backend → Frontend)

Server returns:

-   `200 OK` → ArrayBuffer (`image/png`)
    
-   `400` / `500` → JSON error
    

Example error:

`{  "error":  "Invalid operation",  "message":  "Operation grayscale not found"  }` 

----------

## Example Sharp Operations

`if (operation === "grayscale") {
  processedBuffer = await  sharp(buffer).grayscale().toBuffer();
} if (operation === "rotate") {
  processedBuffer = await  sharp(buffer).rotate(level).toBuffer();
} if (operation === "blur") {
  processedBuffer = await  sharp(buffer).blur(level).toBuffer();
}` 

----------

## Notes

-   Sharp internally outputs PNG unless configured otherwise.
    
-   If deploying on Render, ensure Node version ≥ 16
        
-   Chnage CORS configuration when working with frontend  `app.use(cors());` 
    

----------
## Future Improvements

Here are potential enhancements planned for future versions of this project:

### **Image Processing Enhancements**

-   Add brightness, contrast, hue, and saturation controls
    
-   Introduce cropping tools with preset aspect ratios
    
-   Add flip/mirror operations (horizontal & vertical)
    
-   Implement noise reduction and denoising
    
-   Support advanced filters (sepia, vintage, warm, cool, etc.)
    
-   Allow converting images to multiple formats (PNG, JPG, WEBP)
    
-   Add quality/compression controls
    

### **Editing Workflow Improvements**

-   Support chained operations (multi-step editing)
    
-   Add undo/redo functionality
    
-   Maintain an operation history panel
    
-   Add reset-to-original option
    
-   Add image versioning for better control
    

### **UI/UX Upgrades**

-   Before/After draggable comparison slider
    
-   Drag-and-drop file upload
    
-   Dark mode / Light mode toggle
    
-   More responsive layout for mobile devices
    
-   Add icons/buttons-based editing toolbar
    

### **Deployment & Backend Enhancements**

-   Store images temporarily with auto-cleanup
    
-   Add environment-based configuration (production/dev URLs)
    
-   Rate limiting & file size validation
    
-   Improve backend structure using MVC + TypeScript
    
-   Dockerize backend for easier deployment
    

### **AI-Based Enhancements (Advanced)**

-   AI upscaling (2×/4× resolution enhancement)
    
-   Background removal using ML models
    
-   Automatic image enhancement via AI
    
-   Portrait mode blur using segmentation
    

### **Export & Sharing Features**

-   Choose output format and quality before download
    
-   Support bulk download of processed images
    
-   One-click shareable link to processed image
    
-   Export transformation summary/report


----------
