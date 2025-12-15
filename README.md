<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> फोटो टूल्स</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #e74c3c;
            --light-color: #ecf0f1;
            --dark-color: #2c3e50;
            --success-color: #27ae60;
            --warning-color: #f39c12;
            --info-color: #17a2b8;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            width: 90%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 15px;
        }
        
        /* Header Styles */
        header {
            background-color: var(--primary-color);
            color: white;
            padding: 1rem 0;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            position: sticky;
            top: 0;
            z-index: 1000;
        }
        
        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .logo-icon {
            font-size: 2rem;
            color: var(--secondary-color);
        }
        
        .logo h1 {
            font-size: 1.8rem;
            font-weight: 700;
        }
        
        .logo span {
            color: var(--secondary-color);
        }
        
        nav ul {
            display: flex;
            list-style: none;
            gap: 25px;
        }
        
        nav a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
            padding: 5px 0;
            position: relative;
        }
        
        nav a:hover {
            color: var(--secondary-color);
        }
        
        nav a.active {
            color: var(--secondary-color);
        }
        
        nav a.active::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background-color: var(--secondary-color);
        }
        
        nav a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background-color: var(--secondary-color);
            transition: width 0.3s;
        }
        
        nav a:hover::after {
            width: 100%;
        }
        
        /* Hero Section */
        .hero {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            color: white;
            padding: 4rem 0;
            text-align: center;
            border-radius: 0 0 20px 20px;
            margin-bottom: 3rem;
        }
        
        .hero h2 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            font-weight: 700;
        }
        
        .hero p {
            font-size: 1.2rem;
            max-width: 700px;
            margin: 0 auto 2rem;
            opacity: 0.9;
        }
        
        /* Tool Tabs */
        .tool-tabs {
            display: flex;
            justify-content: center;
            margin-bottom: 2rem;
            background-color: white;
            border-radius: 15px;
            padding: 0.5rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            flex-wrap: wrap;
        }
        
        .tab-btn {
            padding: 12px 20px;
            border: none;
            background: none;
            font-size: 0.9rem;
            font-weight: 600;
            color: var(--dark-color);
            cursor: pointer;
            border-radius: 10px;
            transition: all 0.3s;
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            min-width: 160px;
            margin: 2px;
        }
        
        .tab-btn:hover {
            background-color: rgba(52, 152, 219, 0.1);
        }
        
        .tab-btn.active {
            background-color: var(--secondary-color);
            color: white;
        }
        
        /* Tool Containers */
        .tool-container {
            display: none;
        }
        
        .tool-container.active {
            display: block;
        }
        
        /* Main Content */
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 4rem;
        }
        
        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        /* Upload Section */
        .upload-section {
            background-color: white;
            border-radius: 15px;
            padding: 2rem;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
        }
        
        .section-title {
            font-size: 1.5rem;
            color: var(--primary-color);
            margin-bottom: 1.5rem;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--light-color);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .section-title i {
            color: var(--secondary-color);
        }
        
        .upload-area {
            border: 3px dashed var(--light-color);
            border-radius: 10px;
            padding: 3rem 1rem;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            margin-bottom: 1.5rem;
        }
        
        .upload-area:hover {
            border-color: var(--secondary-color);
            background-color: rgba(52, 152, 219, 0.05);
        }
        
        .upload-area i {
            font-size: 3rem;
            color: var(--secondary-color);
            margin-bottom: 1rem;
        }
        
        .upload-area p {
            margin-bottom: 0.5rem;
            font-weight: 500;
        }
        
        .upload-area span {
            font-size: 0.9rem;
            color: #666;
        }
        
        .fileInput {
            display: none;
        }
        
        .controls {
            margin-top: 2rem;
        }
        
        .control-group {
            margin-bottom: 1.5rem;
        }
        
        .control-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 500;
            color: var(--dark-color);
        }
        
        .slider-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .slider-container span {
            font-weight: 600;
            min-width: 40px;
            text-align: center;
            color: var(--secondary-color);
        }
        
        input[type="range"] {
            width: 100%;
            height: 8px;
            -webkit-appearance: none;
            background: var(--light-color);
            border-radius: 5px;
            outline: none;
        }
        
        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 22px;
            height: 22px;
            background: var(--secondary-color);
            border-radius: 50%;
            cursor: pointer;
        }
        
        .checkbox-group {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 1rem;
        }
        
        .checkbox-group input[type="checkbox"] {
            width: 18px;
            height: 18px;
            cursor: pointer;
        }
        
        .checkbox-group label {
            margin-bottom: 0;
            cursor: pointer;
        }
        
        .buttons {
            display: flex;
            gap: 15px;
            margin-top: 2rem;
        }
        
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            flex: 1;
        }
        
        .btn-primary {
            background-color: var(--secondary-color);
            color: white;
        }
        
        .btn-primary:hover {
            background-color: #2980b9;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.3);
        }
        
        .btn-secondary {
            background-color: var(--light-color);
            color: var(--dark-color);
        }
        
        .btn-secondary:hover {
            background-color: #d5dbdb;
            transform: translateY(-3px);
        }
        
        .btn-warning {
            background-color: var(--warning-color);
            color: white;
        }
        
        .btn-warning:hover {
            background-color: #e67e22;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(243, 156, 18, 0.3);
        }
        
        .btn-success {
            background-color: var(--success-color);
            color: white;
        }
        
        .btn-success:hover {
            background-color: #219653;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(39, 174, 96, 0.3);
        }
        
        .btn-info {
            background-color: var(--info-color);
            color: white;
        }
        
        .btn-info:hover {
            background-color: #138496;
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(23, 162, 184, 0.3);
        }
        
        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none !important;
            box-shadow: none !important;
        }
        
        /* Preview Section */
        .preview-section {
            background-color: white;
            border-radius: 15px;
            padding: 2rem;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
        }
        
        .image-container {
            display: flex;
            flex-direction: column;
            gap: 20px;
            margin-bottom: 2rem;
        }
        
        @media (min-width: 992px) {
            .image-container {
                flex-direction: row;
            }
        }
        
        .image-box {
            flex: 1;
            text-align: center;
        }
        
        .image-box h3 {
            margin-bottom: 1rem;
            color: var(--primary-color);
            font-size: 1.2rem;
        }
        
        .image-placeholder {
            width: 100%;
            height: 250px;
            background-color: var(--light-color);
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #777;
            overflow: hidden;
        }
        
        .image-placeholder img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
        }
        
        .pdf-preview-container {
            width: 100%;
            height: 250px;
            background-color: var(--light-color);
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #777;
            overflow: auto;
            padding: 1rem;
        }
        
        .pdf-page-preview {
            max-width: 100%;
            max-height: 200px;
            margin-bottom: 10px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
        }
        
        .image-info {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            font-size: 0.9rem;
            color: #666;
        }
        
        .compression-stats {
            background-color: #f8f9fa;
            border-radius: 10px;
            padding: 1.5rem;
            margin-top: 2rem;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }
        
        .stat-item {
            text-align: center;
            padding: 15px;
            border-radius: 8px;
            background-color: white;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
        }
        
        .stat-value {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--secondary-color);
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 0.9rem;
            color: #666;
        }
        
        .conversion-stats {
            background-color: #f8f9fa;
            border-radius: 10px;
            padding: 1.5rem;
            margin-top: 2rem;
        }
        
        .conversion-info {
            text-align: center;
            padding: 15px;
            border-radius: 8px;
            background-color: white;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
            margin-bottom: 1rem;
        }
        
        /* Features Section */
        .features {
            margin-bottom: 4rem;
        }
        
        .features h2 {
            text-align: center;
            font-size: 2rem;
            color: var(--primary-color);
            margin-bottom: 3rem;
        }
        
        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 25px;
        }
        
        .feature-card {
            background-color: white;
            border-radius: 15px;
            padding: 2rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            text-align: center;
            transition: transform 0.3s;
        }
        
        .feature-card:hover {
            transform: translateY(-10px);
        }
        
        .feature-icon {
            font-size: 2.5rem;
            color: var(--secondary-color);
            margin-bottom: 1.5rem;
        }
        
        .feature-card h3 {
            font-size: 1.3rem;
            margin-bottom: 1rem;
            color: var(--primary-color);
        }
        
        /* Footer */
        footer {
            background-color: var(--primary-color);
            color: white;
            padding: 3rem 0 1.5rem;
            margin-top: 3rem;
        }
        
        .footer-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
            margin-bottom: 2rem;
        }
        
        .footer-logo h2 {
            font-size: 1.8rem;
            margin-bottom: 1rem;
        }
        
        .footer-logo span {
            color: var(--secondary-color);
        }
        
        .footer-links h3, .footer-contact h3 {
            font-size: 1.3rem;
            margin-bottom: 1.5rem;
            color: var(--secondary-color);
        }
        
        .footer-links ul {
            list-style: none;
        }
        
        .footer-links li {
            margin-bottom: 10px;
        }
        
        .footer-links a {
            color: #ddd;
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .footer-links a:hover {
            color: var(--secondary-color);
        }
        
        .footer-contact p {
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .copyright {
            text-align: center;
            padding-top: 1.5rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
            color: #aaa;
        }
        
        /* Utility Classes */
        .hidden {
            display: none;
        }
        
        .loading {
            position: relative;
            pointer-events: none;
            opacity: 0.7;
        }
        
        .loading::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 20px;
            height: 20px;
            border: 3px solid #f3f3f3;
            border-top: 3px solid var(--secondary-color);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin-left: -10px;
            margin-top: -10px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* PDF Pages Preview */
        .pdf-pages-preview {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 1rem;
            max-height: 200px;
            overflow-y: auto;
            padding: 10px;
            background-color: #f8f9fa;
            border-radius: 8px;
        }
        
        .pdf-page-thumb {
            width: 80px;
            height: 100px;
            background-color: white;
            border-radius: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            position: relative;
        }
        
        .pdf-page-thumb img {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
        }
        
        .page-number {
            position: absolute;
            bottom: 0;
            right: 0;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            font-size: 0.7rem;
            padding: 2px 5px;
            border-radius: 3px 0 0 0;
        }
        
        .page-selector {
            margin-top: 1rem;
            padding: 10px;
            background-color: #f8f9fa;
            border-radius: 8px;
        }
        
        .page-selector label {
            display: block;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        .page-selector input {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 10px;
        }
        
        .page-selector .hint {
            font-size: 0.8rem;
            color: #666;
            margin-top: 5px;
        }
        
        /* File List */
        .file-list {
            margin-top: 1.5rem;
            max-height: 200px;
            overflow-y: auto;
            padding: 10px;
            background-color: #f8f9fa;
            border-radius: 8px;
        }
        
        .file-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 8px 12px;
            background-color: white;
            border-radius: 5px;
            margin-bottom: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
        }
        
        .file-item:last-child {
            margin-bottom: 0;
        }
        
        .file-name {
            flex: 1;
            font-size: 0.9rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }
        
        .file-size {
            font-size: 0.8rem;
            color: #666;
            margin-left: 10px;
        }
        
        .remove-file {
            background: none;
            border: none;
            color: var(--accent-color);
            cursor: pointer;
            font-size: 1rem;
            margin-left: 10px;
        }
        
        /* Page Layout Options */
        .layout-options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-top: 1rem;
        }
        
        .layout-option {
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .layout-option:hover {
            border-color: var(--secondary-color);
            background-color: rgba(52, 152, 219, 0.05);
        }
        
        .layout-option.active {
            border-color: var(--secondary-color);
            background-color: rgba(52, 152, 219, 0.1);
        }
        
        .layout-option i {
            font-size: 1.5rem;
            margin-bottom: 5px;
            color: var(--secondary-color);
        }
        
        /* Image Grid Preview */
        .image-grid-preview {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 8px;
            margin-top: 1rem;
            max-height: 200px;
            overflow-y: auto;
            padding: 10px;
            background-color: #f8f9fa;
            border-radius: 8px;
        }
        
        .image-grid-item {
            position: relative;
            width: 100%;
            padding-bottom: 100%; /* Square aspect ratio */
            background-color: white;
            border-radius: 5px;
            overflow: hidden;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        
        .image-grid-item img {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .image-number {
            position: absolute;
            top: 5px;
            right: 5px;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            font-size: 0.7rem;
            padding: 2px 5px;
            border-radius: 3px;
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container header-container">
            <div class="logo">
                <div class="logo-icon">
                    <i class="fas fa-tools"></i>
                </div>
                <h1>SUJIT <span>CSC CYBER</span></h1>
            </div>
            <nav>
                <ul>
                    <li><a href="#home" class="active">होम</a></li>
                    <li><a href="#features">सुविधाएँ</a></li>
                    <li><a href="#contact">संपर्क</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero" id="home">
        <div class="container">
            <h2>फोटो और PDF टूल्स</h2>
            <p>आपकी तस्वीरों और PDF फाइलों के लिए सर्वोत्तम टूल्स। तेज़, सुरक्षित और मुफ्त सेवाएं।</p>
        </div>
    </section>

    <!-- Tool Tabs -->
    <div class="container">
        <div class="tool-tabs">
            <button class="tab-btn active" id="photoTabBtn" data-tool="photo">
                <i class="fas fa-compress-alt"></i> फोटो कॉम्प्रेसर
            </button>
            <button class="tab-btn" id="pdfTabBtn" data-tool="pdf">
                <i class="fas fa-file-pdf"></i> PDF से PNG
            </button>
            <button class="tab-btn" id="pngToPdfTabBtn" data-tool="pngToPdf">
                <i class="fas fa-images"></i> PNG से PDF
            </button>
            <button class="tab-btn" id="pdfToJpgTabBtn" data-tool="pdfToJpg">
            </button>
        </div>
    </div>

    <!-- Photo Compressor Tool -->
    <div class="container">
        <div class="tool-container active" id="photoTool">
            <div class="main-content">
                <!-- Upload Section -->
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-cloud-upload-alt"></i> फोटो अपलोड करें</h2>
                    
                    <div class="upload-area" id="photoUploadArea">
                        <i class="fas fa-file-image"></i>
                        <p>क्लिक करें या फोटो यहाँ खींचें</p>
                        <span>JPG, PNG, WebP (अधिकतम आकार: 5MB)</span>
                        <input type="file" id="photoFileInput" class="fileInput" accept="image/*">
                    </div>
                    
                    <div class="controls">
                        <div class="control-group">
                            <label for="quality">क्वालिटी स्तर: <span id="qualityValue">70</span>%</label>
                            <div class="slider-container">
                                <span>0</span>
                                <input type="range" id="quality" min="0" max="100" value="70">
                                <span>100</span>
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label for="maxWidth">अधिकतम चौड़ाई: <span id="widthValue">1200</span>px</label>
                            <div class="slider-container">
                                <span>300</span>
                                <input type="range" id="maxWidth" min="300" max="2000" value="1200" step="50">
                                <span>2000</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="buttons">
                        <button class="btn btn-primary" id="compressBtn">
                            <i class="fas fa-compress-alt"></i> कॉम्प्रेस करें
                        </button>
                        <button class="btn btn-secondary" id="resetPhotoBtn">
                            <i class="fas fa-redo"></i> रीसेट करें
                        </button>
                    </div>
                </section>
                
                <!-- Preview Section -->
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> प्रीव्यू और डाउनलोड</h2>
                    
                    <div class="image-container">
                        <div class="image-box">
                            <h3>मूल फोटो</h3>
                            <div class="image-placeholder" id="originalImage">
                                <i class="fas fa-image" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                                <p>फोटो अपलोड करने पर यहाँ दिखेगा</p>
                            </div>
                            <div class="image-info">
                                <span id="originalSize">आकार: --</span>
                                <span id="originalDimensions">डाइमेंशन: --</span>
                            </div>
                        </div>
                        
                        <div class="image-box">
                            <h3>कम्प्रेस्ड फोटो</h3>
                            <div class="image-placeholder" id="compressedImage">
                                <i class="fas fa-file-archive" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                                <p>कम्प्रेस्ड फोटो यहाँ दिखेगा</p>
                            </div>
                            <div class="image-info">
                                <span id="compressedSize">आकार: --</span>
                                <span id="compressedDimensions">डाइमेंशन: --</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="compression-stats">
                        <div class="stats-grid">
                            <div class="stat-item">
                                <div class="stat-value" id="sizeReduction">--</div>
                                <div class="stat-label">आकार कमी</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-value" id="compressionRatio">--</div>
                                <div class="stat-label">कम्प्रेशन अनुपात</div>
                            </div>
                        </div>
                        
                        <div class="buttons" style="margin-top: 1.5rem;">
                            <button class="btn btn-primary" id="downloadPhotoBtn" disabled>
                                <i class="fas fa-download"></i> डाउनलोड करें
                            </button>
                        </div>
                    </div>
                </section>
            </div>
        </div>

        <!-- PDF to PNG Converter Tool -->
        <div class="tool-container" id="pdfTool">
            <div class="main-content">
                <!-- Upload Section -->
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-file-upload"></i> PDF अपलोड करें</h2>
                    
                    <div class="upload-area" id="pdfUploadArea">
                        <i class="fas fa-file-pdf"></i>
                        <p>क्लिक करें या PDF यहाँ खींचें</p>
                        <span>PDF फाइलें (अधिकतम आकार: 10MB)</span>
                        <input type="file" id="pdfFileInput" class="fileInput" accept=".pdf,application/pdf">
                    </div>
                    
                    <div class="controls">
                        <div class="control-group">
                            <label for="pdfQuality">PNG क्वालिटी: <span id="pdfQualityValue">90</span>%</label>
                            <div class="slider-container">
                                <span>10</span>
                                <input type="range" id="pdfQuality" min="10" max="100" value="90">
                                <span>100</span>
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label for="pdfScale">स्केल फैक्टर: <span id="pdfScaleValue">2.0</span>x</label>
                            <div class="slider-container">
                                <span>0.5</span>
                                <input type="range" id="pdfScale" min="0.5" max="3" value="2" step="0.1">
                                <span>3.0</span>
                            </div>
                            <small>उच्च स्केल = बेहतर रिज़ॉल्यूशन, लेकिन बड़ी फाइल</small>
                        </div>
                        
                        <div class="checkbox-group">
                            <input type="checkbox" id="convertAllPages" checked>
                            <label for="convertAllPages">सभी पेज कन्वर्ट करें</label>
                        </div>
                        
                        <div class="page-selector" id="pageSelector" style="display: none;">
                            <label for="pageRange">पेज रेंज (उदा: 1, 1-3, 1,3,5):</label>
                            <input type="text" id="pageRange" placeholder="सभी पेज">
                            <div class="hint">खाली छोड़ने पर सभी पेज कन्वर्ट होंगे</div>
                        </div>
                    </div>
                    
                    <div class="buttons">
                        <button class="btn btn-primary" id="convertPdfBtn">
                            <i class="fas fa-sync-alt"></i> PNG में कन्वर्ट करें
                        </button>
                        <button class="btn btn-secondary" id="resetPdfBtn">
                            <i class="fas fa-redo"></i> रीसेट करें
                        </button>
                    </div>
                </section>
                
                <!-- Preview Section -->
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> PDF प्रीव्यू और रिजल्ट</h2>
                    
                    <div class="image-container">
                        <div class="image-box">
                            <h3>PDF प्रीव्यू</h3>
                            <div class="pdf-preview-container" id="pdfPreview">
                                <i class="fas fa-file-pdf" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                                <p>PDF अपलोड करने पर यहाँ दिखेगा</p>
                            </div>
                            <div class="image-info">
                                <span id="pdfFileSize">आकार: --</span>
                                <span id="pdfPageCount">पेज: --</span>
                            </div>
                        </div>
                        
                        <div class="image-box">
                            <h3>PNG रिजल्ट</h3>
                            <div class="image-placeholder" id="pngResult">
                                <i class="fas fa-image" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                                <p>कन्वर्टेड PNG यहाँ दिखेगा</p>
                            </div>
                            <div class="image-info">
                                <span id="pngCount">PNG: --</span>
                                <span id="pngTotalSize">कुल आकार: --</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="conversion-stats">
                        <div class="conversion-info" id="conversionInfo">
                            <p>PDF अपलोड करें और PNG में कन्वर्ट करने के लिए बटन दबाएं</p>
                        </div>
                        
                        <div class="buttons">
                            <button class="btn btn-primary" id="downloadAllBtn" disabled>
                                <i class="fas fa-download"></i> सभी PNG डाउनलोड करें (ZIP)
                            </button>
                            <button class="btn btn-warning" id="downloadSingleBtn" disabled>
                                <i class="fas fa-file-download"></i> पहला PNG डाउनलोड करें
                            </button>
                        </div>
                    </div>
                </section>
            </div>
        </div>

        <!-- PNG to PDF Converter Tool -->
        <div class="tool-container" id="pngToPdfTool">
            <div class="main-content">
                <!-- Upload Section -->
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-images"></i> PNG इमेजेस अपलोड करें</h2>
                    
                    <div class="upload-area" id="pngToPdfUploadArea">
                        <i class="fas fa-file-image"></i>
                        <p>क्लिक करें या PNG इमेजेस यहाँ खींचें</p>
                        <span>PNG फाइलें (अधिकतम 20 इमेजेस, प्रत्येक 5MB)</span>
                        <input type="file" id="pngToPdfFileInput" class="fileInput" accept=".png,image/png" multiple>
                    </div>
                    
                    <!-- File List -->
                    <div class="file-list" id="pngFileList" style="display: none;">
                        <!-- Files will be added here dynamically -->
                    </div>
                    
                    <div class="controls">
                        <div class="control-group">
                            <label>पेज लेआउट:</label>
                            <div class="layout-options">
                                <div class="layout-option active" data-layout="portrait">
                                    <i class="fas fa-portrait"></i>
                                    <div>पोर्ट्रेट</div>
                                </div>
                                <div class="layout-option" data-layout="landscape">
                                    <i class="fas fa-landscape"></i>
                                    <div>लैंडस्केप</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label for="pageSize">पेज साइज:</label>
                            <select id="pageSize" class="slider-container" style="width: 100%; padding: 8px; border: 1px solid #ddd; border-radius: 5px;">
                                <option value="a4">A4</option>
                                <option value="letter">Letter</option>
                                <option value="legal">Legal</option>
                                <option value="a3">A3</option>
                            </select>
                        </div>
                        
                        <div class="control-group">
                            <label for="imageQuality">इमेज क्वालिटी: <span id="imageQualityValue">90</span>%</label>
                            <div class="slider-container">
                                <span>10</span>
                                <input type="range" id="imageQuality" min="10" max="100" value="90">
                                <span>100</span>
                            </div>
                        </div>
                        
                        <div class="checkbox-group">
                            <input type="checkbox" id="addPageNumbers" checked>
                            <label for="addPageNumbers">पेज नंबर जोड़ें</label>
                        </div>
                    </div>
                    
                    <div class="buttons">
                        <button class="btn btn-success" id="convertToPdfBtn">
                            <i class="fas fa-file-pdf"></i> PDF बनाएं
                        </button>
                        <button class="btn btn-secondary" id="resetPngToPdfBtn">
                            <i class="fas fa-redo"></i> रीसेट करें
                        </button>
                    </div>
                </section>
                
                <!-- Preview Section -->
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> इमेजेस प्रीव्यू और PDF</h2>
                    
                    <div class="image-container">
                        <div class="image-box">
                            <h3>इमेजेस प्रीव्यू</h3>
                            <div class="image-grid-preview" id="pngImagesPreview">
                                <div class="image-placeholder">
                                    <i class="fas fa-images" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                                    <p>PNG इमेजेस अपलोड करने पर यहाँ दिखेंगी</p>
                                </div>
                            </div>
                            <div class="image-info">
                                <span id="pngImagesCount">इमेजेस: 0</span>
                                <span id="pngImagesTotalSize">कुल आकार: --</span>
                            </div>
                        </div>
                        
                        <div class="image-box">
                            <h3>PDF रिजल्ट</h3>
                            <div class="pdf-preview-container" id="pdfResult">
                                <i class="fas fa-file-pdf" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                                <p>कन्वर्टेड PDF यहाँ दिखेगा</p>
                            </div>
                            <div class="image-info">
                                <span id="pdfResultSize">आकार: --</span>
                                <span id="pdfResultPages">पेज: --</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="conversion-stats">
                        <div class="conversion-info" id="pngToPdfConversionInfo">
                            <p>PNG इमेजेस अपलोड करें और PDF बनाने के लिए बटन दबाएं</p>
                        </div>
                        
                        <div class="buttons">
                            <button class="btn btn-primary" id="downloadPdfBtn" disabled>
                                <i class="fas fa-download"></i> PDF डाउनलोड करें
                            </button>
                        </div>
                    </div>
                </section>
            </div>
        </div>

        <!-- PDF to JPG Converter Tool -->
        <div class="tool-container" id="pdfToJpgTool">
            <div class="main-content">
                <!-- Upload Section -->
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-file-upload"></i> PDF अपलोड करें</h2>
                    
                    <div class="upload-area" id="pdfToJpgUploadArea">
                        <i class="fas fa-file-pdf"></i>
                        <p>क्लिक करें या PDF यहाँ खींचें</p>
                        <span>PDF फाइलें (अधिकतम आकार: 10MB)</span>
                        <input type="file" id="pdfToJpgFileInput" class="fileInput" accept=".pdf,application/pdf">
                    </div>
                    
                    <div class="controls">
                        <div class="control-group">
                            <label for="jpgQuality">JPG क्वालिटी: <span id="jpgQualityValue">85</span>%</label>
                            <div class="slider-container">
                                <span>10</span>
                                <input type="range" id="jpgQuality" min="10" max="100" value="85">
                                <span>100</span>
                            </div>
                        </div>
                        
                        <div class="control-group">
                            <label for="jpgScale">स्केल फैक्टर: <span id="jpgScaleValue">1.5</span>x</label>
                            <div class="slider-container">
                                <span>0.5</span>
                                <input type="range" id="jpgScale" min="0.5" max="3" value="1.5" step="0.1">
                                <span>3.0</span>
                            </div>
                            <small>उच्च स्केल = बेहतर रिज़ॉल्यूशन, लेकिन बड़ी फाइल</small>
                        </div>
                        
                        <div class="checkbox-group">
                            <input type="checkbox" id="convertAllPagesToJpg" checked>
                            <label for="convertAllPagesToJpg">सभी पेज कन्वर्ट करें</label>
                        </div>
                        
                        <div class="page-selector" id="pdfToJpgPageSelector" style="display: none;">
                            <label for="pdfToJpgPageRange">पेज रेंज (उदा: 1, 1-3, 1,3,5):</label>
                            <input type="text" id="pdfToJpgPageRange" placeholder="सभी पेज">
                            <div class="hint">खाली छोड़ने पर सभी पेज कन्वर्ट होंगे</div>
                        </div>
                    </div>
                    
                    <div class="buttons">
                        <button class="btn btn-info" id="convertPdfToJpgBtn">
                            <i class="fas fa-sync-alt"></i> JPG में कन्वर्ट करें
                        </button>
                        <button class="btn btn-secondary" id="resetPdfToJpgBtn">
                            <i class="fas fa-redo"></i> रीसेट करें
                        </button>
                    </div>
                </section>
                
                <!-- Preview Section -->
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> PDF प्रीव्यू और JPG रिजल्ट</h2>
                    
                    <div class="image-container">
                        <div class="image-box">
                            <h3>PDF प्रीव्यू</h3>
                            <div class="pdf-preview-container" id="pdfToJpgPreview">
                                <i class="fas fa-file-pdf" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                                <p>PDF अपलोड करने पर यहाँ दिखेगा</p>
                            </div>
                            <div class="image-info">
                                <span id="pdfToJpgFileSize">आकार: --</span>
                                <span id="pdfToJpgPageCount">पेज: --</span>
                            </div>
                        </div>
                        
                        <div class="image-box">
                            <h3>JPG रिजल्ट</h3>
                            <div class="image-placeholder" id="jpgResult">
                                <i class="fas fa-image" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                                <p>कन्वर्टेड JPG यहाँ दिखेगा</p>
                            </div>
                            <div class="image-info">
                                <span id="jpgCount">JPG: --</span>
                                <span id="jpgTotalSize">कुल आकार: --</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="conversion-stats">
                        <div class="conversion-info" id="pdfToJpgConversionInfo">
                            <p>PDF अपलोड करें और JPG में कन्वर्ट करने के लिए बटन दबाएं</p>
                        </div>
                        
                        <div class="buttons">
                            <button class="btn btn-primary" id="downloadAllJpgBtn" disabled>
                                <i class="fas fa-download"></i> सभी JPG डाउनलोड करें (ZIP)
                            </button>
                            <button class="btn btn-warning" id="downloadSingleJpgBtn" disabled>
                                <i class="fas fa-file-download"></i> पहला JPG डाउनलोड करें
                            </button>
                        </div>
                    </div>
                </section>
            </div>
        </div>
        
        <!-- Features Section -->
        <section class="features" id="features">
            <h2>हमारी विशेषताएँ</h2>
            <div class="features-grid">
                <div class="feature-card">
                    <div class="feature-icon">
                        <i class="fas fa-bolt"></i>
                    </div>
                    <h3>तेज़ प्रोसेसिंग</h3>
                    <p>हमारे उन्नत एल्गोरिदम सेकंडों में आपकी तस्वीरों और PDF को प्रोसेस कर देते हैं।</p>
                </div>
                
                <div class="feature-card">
                    <div class="feature-icon">
                        <i class="fas fa-shield-alt"></i>
                    </div>
                    <h3>सुरक्षित</h3>
                    <p>आपकी फाइलें हमारे सर्वर पर कभी संग्रहीत नहीं की जाती हैं। सभी प्रक्रिया आपके ब्राउज़र में होती है।</p>
                </div>
                
                <div class="feature-card">
                    <div class="feature-icon">
                        <i class="fas fa-chart-line"></i>
                    </div>
                    <h3>उच्च गुणवत्ता</h3>
                    <p>फोटो और PDF कन्वर्जन में उच्च गुणवत्ता बनाए रखते हुए आपकी फाइलों को प्रोसेस करें।</p>
                </div>
                
                <div class="feature-card">
                    <div class="feature-icon">
                        <i class="fas fa-tools"></i>
                    </div>
                    <h3>मल्टीपल टूल्स</h3>
                    <p>फोटो कंप्रेशन से लेकर PDF कन्वर्जन तक, सभी जरूरी टूल्स एक ही जगह पर।</p>
                </div>
            </div>
        </section>
    </div>

    <!-- Footer -->
    <footer id="contact">
        <div class="container">
            <div class="footer-container">
                <div class="footer-logo">
                    <h2>SUJIT <span>CSC CYBER</span></h2>
                    <p>आपकी तस्वीरों और PDF के लिए सर्वोत्तम टूल्स समाधान।</p>
                </div>
                
                <div class="footer-links">
                    <h3>टूल्स</h3>
                    <ul>
                        <li><a href="#" id="photoToolLink">फोटो कॉम्प्रेसर</a></li>
                        <li><a href="#" id="pdfToolLink">PDF से PNG</a></li>
                        <li><a href="#" id="pngToPdfToolLink">PNG से PDF</a></li>
                        <li><a href="#" id="pdfToJpgToolLink">PDF से JPG</a></li>
                        <li><a href="#features">सुविधाएँ</a></li>
                        <li><a href="#contact">संपर्क</a></li>
                    </ul>
                </div>
                
                <div class="footer-contact">
                    <h3>संपर्क करें</h3>
                    <p><i class="fas fa-map-marker-alt"></i> बसंत पट्टी</p>
                    <p><i class="fas fa-phone"></i> +91 72098 90909</p>
                    <p><i class="fas fa-envelope"></i> sujitcsc cyber@gmail.com</p>
                </div>
            </div>
            
            <div class="copyright">
                <p>&copy; 2025 SUJIT CSC CYBER. सर्वाधिकार सुरक्षित।</p>
            </div>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // ============================================
            // Tool Tabs Functionality
            // ============================================
            const photoTabBtn = document.getElementById('photoTabBtn');
            const pdfTabBtn = document.getElementById('pdfTabBtn');
            const pngToPdfTabBtn = document.getElementById('pngToPdfTabBtn');
            const pdfToJpgTabBtn = document.getElementById('pdfToJpgTabBtn');
            const photoTool = document.getElementById('photoTool');
            const pdfTool = document.getElementById('pdfTool');
            const pngToPdfTool = document.getElementById('pngToPdfTool');
            const pdfToJpgTool = document.getElementById('pdfToJpgTool');
            
            const photoToolLink = document.getElementById('photoToolLink');
            const pdfToolLink = document.getElementById('pdfToolLink');
            const pngToPdfToolLink = document.getElementById('pngToPdfToolLink');
            const pdfToJpgToolLink = document.getElementById('pdfToJpgToolLink');
            
            // Function to show a specific tool and hide others
            function showTool(toolId) {
                // Remove active class from all tabs
                [photoTabBtn, pdfTabBtn, pngToPdfTabBtn, pdfToJpgTabBtn].forEach(btn => {
                    btn.classList.remove('active');
                });
                
                // Hide all tool containers
                [photoTool, pdfTool, pngToPdfTool, pdfToJpgTool].forEach(tool => {
                    tool.classList.remove('active');
                });
                
                // Activate the selected tab
                document.getElementById(toolId + 'TabBtn').classList.add('active');
                
                // Show the selected tool
                document.getElementById(toolId + 'Tool').classList.add('active');
            }
            
            // Event listeners for tabs
            photoTabBtn.addEventListener('click', () => showTool('photo'));
            pdfTabBtn.addEventListener('click', () => showTool('pdf'));
            pngToPdfTabBtn.addEventListener('click', () => showTool('pngToPdf'));
            pdfToJpgTabBtn.addEventListener('click', () => showTool('pdfToJpg'));
            
            // Event listeners for footer links
            photoToolLink.addEventListener('click', function(e) {
                e.preventDefault();
                showTool('photo');
            });
            pdfToolLink.addEventListener('click', function(e) {
                e.preventDefault();
                showTool('pdf');
            });
            pngToPdfToolLink.addEventListener('click', function(e) {
                e.preventDefault();
                showTool('pngToPdf');
            });
            pdfToJpgToolLink.addEventListener('click', function(e) {
                e.preventDefault();
                showTool('pdfToJpg');
            });
            
            // ============================================
            // Photo Compression Tool (Existing Code)
            // ============================================
            // [Existing photo compression code remains the same]
            // ... (photo compression code from original)
            
            // ============================================
            // PDF to PNG Converter Tool (Existing Code)
            // ============================================
            // [Existing PDF to PNG code remains the same]
            // ... (PDF to PNG code from original)
            
            // ============================================
            // PNG to PDF Converter Tool (New Code)
            // ============================================
            const pngToPdfFileInput = document.getElementById('pngToPdfFileInput');
            const pngToPdfUploadArea = document.getElementById('pngToPdfUploadArea');
            const pngFileList = document.getElementById('pngFileList');
            const pngImagesPreview = document.getElementById('pngImagesPreview');
            const convertToPdfBtn = document.getElementById('convertToPdfBtn');
            const resetPngToPdfBtn = document.getElementById('resetPngToPdfBtn');
            const downloadPdfBtn = document.getElementById('downloadPdfBtn');
            const pngImagesCount = document.getElementById('pngImagesCount');
            const pngImagesTotalSize = document.getElementById('pngImagesTotalSize');
            const pdfResultSize = document.getElementById('pdfResultSize');
            const pdfResultPages = document.getElementById('pdfResultPages');
            const pngToPdfConversionInfo = document.getElementById('pngToPdfConversionInfo');
            const imageQualitySlider = document.getElementById('imageQuality');
            const imageQualityValue = document.getElementById('imageQualityValue');
            const layoutOptions = document.querySelectorAll('.layout-option');
            const pageSizeSelect = document.getElementById('pageSize');
            const addPageNumbersCheckbox = document.getElementById('addPageNumbers');
            
            // State variables for PNG to PDF tool
            let pngFiles = [];
            let pdfBlob = null;
            
            // Event Listeners for PNG to PDF tool
            pngToPdfUploadArea.addEventListener('click', () => pngToPdfFileInput.click());
            pngToPdfUploadArea.addEventListener('dragover', (e) => {
                e.preventDefault();
                pngToPdfUploadArea.style.borderColor = '#3498db';
                pngToPdfUploadArea.style.backgroundColor = 'rgba(52, 152, 219, 0.1)';
            });
            pngToPdfUploadArea.addEventListener('dragleave', () => {
                pngToPdfUploadArea.style.borderColor = '#ecf0f1';
                pngToPdfUploadArea.style.backgroundColor = 'transparent';
            });
            pngToPdfUploadArea.addEventListener('drop', (e) => {
                e.preventDefault();
                pngToPdfUploadArea.style.borderColor = '#ecf0f1';
                pngToPdfUploadArea.style.backgroundColor = 'transparent';
                
                if (e.dataTransfer.files.length) {
                    handlePngFilesSelect(Array.from(e.dataTransfer.files));
                }
            });
            
            pngToPdfFileInput.addEventListener('change', (e) => {
                if (e.target.files.length) {
                    handlePngFilesSelect(Array.from(e.target.files));
                }
            });
            
            imageQualitySlider.addEventListener('input', () => {
                imageQualityValue.textContent = imageQualitySlider.value;
            });
            
            // Layout options selection
            layoutOptions.forEach(option => {
                option.addEventListener('click', function() {
                    layoutOptions.forEach(opt => opt.classList.remove('active'));
                    this.classList.add('active');
                });
            });
            
            convertToPdfBtn.addEventListener('click', convertPngToPdf);
            resetPngToPdfBtn.addEventListener('click', resetPngToPdf);
            downloadPdfBtn.addEventListener('click', downloadPdf);
            
            // Functions for PNG to PDF tool
            function handlePngFilesSelect(files) {
                // Filter only PNG files
                const pngFilesArray = files.filter(file => 
                    file.type === 'image/png' || file.name.toLowerCase().endsWith('.png')
                );
                
                // Check if any PNG files were selected
                if (pngFilesArray.length === 0) {
                    alert('कृपया केवल PNG फाइलें अपलोड करें।');
                    return;
                }
                
                // Check total number of files (max 20)
                const totalFiles = pngFiles.length + pngFilesArray.length;
                if (totalFiles > 20) {
                    alert('आप अधिकतम 20 PNG फाइलें अपलोड कर सकते हैं।');
                    return;
                }
                
                // Check file sizes (max 5MB each)
                for (const file of pngFilesArray) {
                    if (file.size > 5 * 1024 * 1024) {
                        alert(`फाइल "${file.name}" का आकार 5MB से कम होना चाहिए।`);
                        return;
                    }
                }
                
                // Add new files to the array
                pngFiles.push(...pngFilesArray);
                
                // Update UI
                updatePngFilesList();
                updatePngImagesPreview();
                
                // Enable convert button
                convertToPdfBtn.disabled = false;
            }
            
            function updatePngFilesList() {
                // Clear the list
                pngFileList.innerHTML = '';
                
                if (pngFiles.length === 0) {
                    pngFileList.style.display = 'none';
                    return;
                }
                
                pngFileList.style.display = 'block';
                
                // Add each file to the list
                let totalSize = 0;
                pngFiles.forEach((file, index) => {
                    totalSize += file.size;
                    
                    const fileItem = document.createElement('div');
                    fileItem.className = 'file-item';
                    fileItem.innerHTML = `
                        <div class="file-name">${file.name}</div>
                        <div class="file-size">${formatFileSize(file.size)}</div>
                        <button class="remove-file" data-index="${index}">
                            <i class="fas fa-times"></i>
                        </button>
                    `;
                    pngFileList.appendChild(fileItem);
                });
                
                // Update file count and total size
                pngImagesCount.textContent = `इमेजेस: ${pngFiles.length}`;
                pngImagesTotalSize.textContent = `कुल आकार: ${formatFileSize(totalSize)}`;
                
                // Add event listeners to remove buttons
                pngFileList.querySelectorAll('.remove-file').forEach(button => {
                    button.addEventListener('click', function() {
                        const index = parseInt(this.getAttribute('data-index'));
                        removePngFile(index);
                    });
                });
            }
            
            function updatePngImagesPreview() {
                // Clear preview
                pngImagesPreview.innerHTML = '';
                
                if (pngFiles.length === 0) {
                    pngImagesPreview.innerHTML = `
                        <div class="image-placeholder">
                            <i class="fas fa-images" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                            <p>PNG इमेजेस अपलोड करने पर यहाँ दिखेंगी</p>
                        </div>
                    `;
                    return;
                }
                
                // Show first 9 images in grid
                const imagesToShow = pngFiles.slice(0, 9);
                
                imagesToShow.forEach((file, index) => {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        const imgItem = document.createElement('div');
                        imgItem.className = 'image-grid-item';
                        imgItem.innerHTML = `
                            <img src="${e.target.result}" alt="Image ${index + 1}">
                            <div class="image-number">${index + 1}</div>
                        `;
                        pngImagesPreview.appendChild(imgItem);
                    };
                    reader.readAsDataURL(file);
                });
                
                // If there are more than 9 images, show a count
                if (pngFiles.length > 9) {
                    const moreItem = document.createElement('div');
                    moreItem.className = 'image-grid-item';
                    moreItem.style.display = 'flex';
                    moreItem.style.alignItems = 'center';
                    moreItem.style.justifyContent = 'center';
                    moreItem.style.backgroundColor = 'var(--secondary-color)';
                    moreItem.style.color = 'white';
                    moreItem.style.fontWeight = 'bold';
                    moreItem.innerHTML = `+${pngFiles.length - 9} more`;
                    pngImagesPreview.appendChild(moreItem);
                }
            }
            
            function removePngFile(index) {
                pngFiles.splice(index, 1);
                updatePngFilesList();
                updatePngImagesPreview();
                
                // Disable convert button if no files
                if (pngFiles.length === 0) {
                    convertToPdfBtn.disabled = true;
                }
            }
            
            async function convertPngToPdf() {
                if (pngFiles.length === 0) {
                    alert('कृपया पहले PNG इमेजेस अपलोड करें।');
                    return;
                }
                
                // Show loading state
                convertToPdfBtn.classList.add('loading');
                convertToPdfBtn.disabled = true;
                
                try {
                    // Get settings
                    const quality = parseInt(imageQualitySlider.value) / 100;
                    const layout = document.querySelector('.layout-option.active').getAttribute('data-layout');
                    const pageSize = pageSizeSelect.value;
                    const addPageNumbers = addPageNumbersCheckbox.checked;
                    
                    // Create PDF
                    const { jsPDF } = window.jspdf;
                    const pdf = new jsPDF({
                        orientation: layout,
                        unit: 'mm',
                        format: pageSize
                    });
                    
                    // Convert each image to base64 and add to PDF
                    for (let i = 0; i < pngFiles.length; i++) {
                        const file = pngFiles[i];
                        
                        // Convert file to base64
                        const base64 = await fileToBase64(file);
                        
                        // Get image dimensions
                        const img = new Image();
                        await new Promise((resolve) => {
                            img.onload = resolve;
                            img.src = base64;
                        });
                        
                        // Calculate dimensions for PDF
                        const pageWidth = pdf.internal.pageSize.getWidth();
                        const pageHeight = pdf.internal.pageSize.getHeight();
                        
                        let imgWidth = pageWidth - 20; // 10mm margin on each side
                        let imgHeight = (img.height * imgWidth) / img.width;
                        
                        // If image is too tall, scale it down
                        if (imgHeight > pageHeight - 20) {
                            imgHeight = pageHeight - 20;
                            imgWidth = (img.width * imgHeight) / img.height;
                        }
                        
                        // Center the image
                        const x = (pageWidth - imgWidth) / 2;
                        const y = (pageHeight - imgHeight) / 2;
                        
                        // Add image to PDF
                        pdf.addImage(base64, 'PNG', x, y, imgWidth, imgHeight, `image${i}`, 'MEDIUM');
                        
                        // Add page number if enabled
                        if (addPageNumbers) {
                            pdf.setFontSize(10);
                            pdf.text(`Page ${i + 1} of ${pngFiles.length}`, pageWidth / 2, pageHeight - 10, { align: 'center' });
                        }
                        
                        // Add new page if not the last image
                        if (i < pngFiles.length - 1) {
                            pdf.addPage();
                        }
                    }
                    
                    // Generate PDF blob
                    const pdfBlobData = pdf.output('blob');
                    pdfBlob = pdfBlobData;
                    
                    // Display PDF preview
                    const pdfUrl = URL.createObjectURL(pdfBlobData);
                    pdfResult.innerHTML = `
                        <embed src="${pdfUrl}" type="application/pdf" width="100%" height="100%">
                    `;
                    
                    // Update PDF info
                    pdfResultSize.textContent = `आकार: ${formatFileSize(pdfBlobData.size)}`;
                    pdfResultPages.textContent = `पेज: ${pngFiles.length}`;
                    
                    // Update conversion info
                    pngToPdfConversionInfo.innerHTML = `
                        <p><strong>PDF बन गया!</strong></p>
                        <p>${pngFiles.length} PNG इमेजेस PDF में कन्वर्ट हो गईं</p>
                        <p>PDF आकार: ${formatFileSize(pdfBlobData.size)}</p>
                    `;
                    
                    // Enable download button
                    downloadPdfBtn.disabled = false;
                    
                } catch (error) {
                    alert('PNG से PDF बनाने में त्रुटि: ' + error.message);
                } finally {
                    // Remove loading state
                    convertToPdfBtn.classList.remove('loading');
                    convertToPdfBtn.disabled = false;
                }
            }
            
            function downloadPdf() {
                if (!pdfBlob) return;
                
                const link = document.createElement('a');
                link.href = URL.createObjectURL(pdfBlob);
                link.download = `images_to_pdf_${new Date().getTime()}.pdf`;
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            }
            
            function resetPngToPdf() {
                // Reset file input
                pngToPdfFileInput.value = '';
                
                // Reset state variables
                pngFiles = [];
                pdfBlob = null;
                
                // Reset UI
                pngFileList.innerHTML = '';
                pngFileList.style.display = 'none';
                
                pngImagesPreview.innerHTML = `
                    <div class="image-placeholder">
                        <i class="fas fa-images" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                        <p>PNG इमेजेस अपलोड करने पर यहाँ दिखेंगी</p>
                    </div>
                `;
                
                pdfResult.innerHTML = `
                    <i class="fas fa-file-pdf" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                    <p>कन्वर्टेड PDF यहाँ दिखेगा</p>
                `;
                
                pngImagesCount.textContent = 'इमेजेस: 0';
                pngImagesTotalSize.textContent = 'कुल आकार: --';
                pdfResultSize.textContent = 'आकार: --';
                pdfResultPages.textContent = 'पेज: --';
                
                // Reset settings
                imageQualitySlider.value = 90;
                imageQualityValue.textContent = '90';
                
                // Reset layout to portrait
                layoutOptions.forEach(opt => opt.classList.remove('active'));
                document.querySelector('.layout-option[data-layout="portrait"]').classList.add('active');
                
                pageSizeSelect.value = 'a4';
                addPageNumbersCheckbox.checked = true;
                
                // Reset conversion info
                pngToPdfConversionInfo.innerHTML = `
                    <p>PNG इमेजेस अपलोड करें और PDF बनाने के लिए बटन दबाएं</p>
                `;
                
                // Disable buttons
                convertToPdfBtn.disabled = true;
                downloadPdfBtn.disabled = true;
            }
            
            // Helper function to convert file to base64
            function fileToBase64(file) {
                return new Promise((resolve, reject) => {
                    const reader = new FileReader();
                    reader.readAsDataURL(file);
                    reader.onload = () => resolve(reader.result);
                    reader.onerror = error => reject(error);
                });
            }
            
            // ============================================
            // PDF to JPG Converter Tool (New Code)
            // ============================================
            const pdfToJpgFileInput = document.getElementById('pdfToJpgFileInput');
            const pdfToJpgUploadArea = document.getElementById('pdfToJpgUploadArea');
            const pdfToJpgPreview = document.getElementById('pdfToJpgPreview');
            const jpgResult = document.getElementById('jpgResult');
            const convertPdfToJpgBtn = document.getElementById('convertPdfToJpgBtn');
            const resetPdfToJpgBtn = document.getElementById('resetPdfToJpgBtn');
            const downloadAllJpgBtn = document.getElementById('downloadAllJpgBtn');
            const downloadSingleJpgBtn = document.getElementById('downloadSingleJpgBtn');
            const jpgQualitySlider = document.getElementById('jpgQuality');
            const jpgScaleSlider = document.getElementById('jpgScale');
            const jpgQualityValue = document.getElementById('jpgQualityValue');
            const jpgScaleValue = document.getElementById('jpgScaleValue');
            const pdfToJpgFileSize = document.getElementById('pdfToJpgFileSize');
            const pdfToJpgPageCount = document.getElementById('pdfToJpgPageCount');
            const jpgCount = document.getElementById('jpgCount');
            const jpgTotalSize = document.getElementById('jpgTotalSize');
            const pdfToJpgConversionInfo = document.getElementById('pdfToJpgConversionInfo');
            const convertAllPagesToJpgCheckbox = document.getElementById('convertAllPagesToJpg');
            const pdfToJpgPageSelector = document.getElementById('pdfToJpgPageSelector');
            const pdfToJpgPageRange = document.getElementById('pdfToJpgPageRange');
            
            // State variables for PDF to JPG tool
            let pdfToJpgFile = null;
            let pdfToJpgDoc = null;
            let jpgImages = [];
            let jpgBlobs = [];
            
            // Event Listeners for PDF to JPG tool
            pdfToJpgUploadArea.addEventListener('click', () => pdfToJpgFileInput.click());
            pdfToJpgUploadArea.addEventListener('dragover', (e) => {
                e.preventDefault();
                pdfToJpgUploadArea.style.borderColor = '#3498db';
                pdfToJpgUploadArea.style.backgroundColor = 'rgba(52, 152, 219, 0.1)';
            });
            pdfToJpgUploadArea.addEventListener('dragleave', () => {
                pdfToJpgUploadArea.style.borderColor = '#ecf0f1';
                pdfToJpgUploadArea.style.backgroundColor = 'transparent';
            });
            pdfToJpgUploadArea.addEventListener('drop', (e) => {
                e.preventDefault();
                pdfToJpgUploadArea.style.borderColor = '#ecf0f1';
                pdfToJpgUploadArea.style.backgroundColor = 'transparent';
                
                if (e.dataTransfer.files.length) {
                    handlePdfToJpgFileSelect(e.dataTransfer.files[0]);
                }
            });
            
            pdfToJpgFileInput.addEventListener('change', (e) => {
                if (e.target.files.length) {
                    handlePdfToJpgFileSelect(e.target.files[0]);
                }
            });
            
            jpgQualitySlider.addEventListener('input', () => {
                jpgQualityValue.textContent = jpgQualitySlider.value;
            });
            
            jpgScaleSlider.addEventListener('input', () => {
                jpgScaleValue.textContent = jpgScaleSlider.value;
            });
            
            convertPdfToJpgBtn.addEventListener('click', convertPdfToJpg);
            resetPdfToJpgBtn.addEventListener('click', resetPdfToJpgAll);
            downloadAllJpgBtn.addEventListener('click', downloadAllJpgs);
            downloadSingleJpgBtn.addEventListener('click', downloadFirstJpg);
            
            convertAllPagesToJpgCheckbox.addEventListener('change', function() {
                if (this.checked) {
                    pdfToJpgPageSelector.style.display = 'none';
                } else {
                    pdfToJpgPageSelector.style.display = 'block';
                }
            });
            
            // Functions for PDF to JPG tool
            function handlePdfToJpgFileSelect(file) {
                // Check if file is a PDF
                if (!file.type.includes('pdf') && !file.name.toLowerCase().endsWith('.pdf')) {
                    alert('कृपया केवल PDF फाइल अपलोड करें।');
                    return;
                }
                
                // Check file size (10MB limit)
                if (file.size > 10 * 1024 * 1024) {
                    alert('फाइल का आकार 10MB से कम होना चाहिए।');
                    return;
                }
                
                pdfToJpgFile = file;
                
                // Display file info
                pdfToJpgFileSize.textContent = `आकार: ${formatFileSize(file.size)}`;
                
                // Load PDF for preview
                const reader = new FileReader();
                reader.onload = function(e) {
                    const typedarray = new Uint8Array(e.target.result);
                    
                    // Load PDF document
                    pdfjsLib.getDocument(typedarray).promise.then(function(doc) {
                        pdfToJpgDoc = doc;
                        const numPages = doc.numPages;
                        pdfToJpgPageCount.textContent = `पेज: ${numPages}`;
                        
                        // Update conversion info
                        pdfToJpgConversionInfo.innerHTML = `
                            <p><strong>PDF लोड हो गया!</strong></p>
                            <p>कुल पेज: ${numPages}</p>
                            <p>JPG में कन्वर्ट करने के लिए बटन दबाएं</p>
                        `;
                        
                        // Show first page as preview
                        renderPdfToJpgPagePreview(1);
                        
                        // Enable convert button
                        convertPdfToJpgBtn.disabled = false;
                    }).catch(function(error) {
                        alert('PDF लोड करने में त्रुटि: ' + error.message);
                    });
                };
                reader.readAsArrayBuffer(file);
            }
            
            function renderPdfToJpgPagePreview(pageNum) {
                if (!pdfToJpgDoc) return;
                
                pdfToJpgDoc.getPage(pageNum).then(function(page) {
                    const scale = 1.5;
                    const viewport = page.getViewport({ scale: scale });
                    
                    // Prepare canvas for rendering
                    const canvas = document.createElement('canvas');
                    const context = canvas.getContext('2d');
                    canvas.height = viewport.height;
                    canvas.width = viewport.width;
                    
                    // Render PDF page on canvas
                    const renderContext = {
                        canvasContext: context,
                        viewport: viewport
                    };
                    
                    page.render(renderContext).promise.then(function() {
                        // Clear preview and add canvas
                        pdfToJpgPreview.innerHTML = '';
                        canvas.classList.add('pdf-page-preview');
                        pdfToJpgPreview.appendChild(canvas);
                        
                        // Add page info
                        const pageInfo = document.createElement('p');
                        pageInfo.textContent = `पेज ${pageNum} / ${pdfToJpgDoc.numPages}`;
                        pageInfo.style.marginTop = '10px';
                        pageInfo.style.fontSize = '0.9rem';
                        pdfToJpgPreview.appendChild(pageInfo);
                    });
                });
            }
            
            function convertPdfToJpg() {
                if (!pdfToJpgDoc) {
                    alert('कृपया पहले एक PDF अपलोड करें।');
                    return;
                }
                
                // Show loading state
                convertPdfToJpgBtn.classList.add('loading');
                convertPdfToJpgBtn.disabled = true;
                
                // Get conversion settings
                const quality = parseInt(jpgQualitySlider.value) / 100;
                const scale = parseFloat(jpgScaleSlider.value);
                
                // Determine which pages to convert
                let pagesToConvert = [];
                const totalPages = pdfToJpgDoc.numPages;
                
                if (convertAllPagesToJpgCheckbox.checked) {
                    // Convert all pages
                    for (let i = 1; i <= totalPages; i++) {
                        pagesToConvert.push(i);
                    }
                } else {
                    // Parse page range input
                    const pageRange = pdfToJpgPageRange.value.trim();
                    if (pageRange === '') {
                        // Convert all pages if input is empty
                        for (let i = 1; i <= totalPages; i++) {
                            pagesToConvert.push(i);
                        }
                    } else {
                        // Parse page range string (e.g., "1, 1-3, 1,3,5")
                        const parts = pageRange.split(',');
                        for (let part of parts) {
                            part = part.trim();
                            if (part.includes('-')) {
                                // It's a range
                                const rangeParts = part.split('-');
                                const start = parseInt(rangeParts[0].trim());
                                const end = parseInt(rangeParts[1].trim());
                                
                                if (!isNaN(start) && !isNaN(end) && start <= end) {
                                    for (let i = start; i <= end; i++) {
                                        if (i >= 1 && i <= totalPages) {
                                            pagesToConvert.push(i);
                                        }
                                    }
                                }
                            } else {
                                // It's a single page
                                const pageNum = parseInt(part);
                                if (!isNaN(pageNum) && pageNum >= 1 && pageNum <= totalPages) {
                                    pagesToConvert.push(pageNum);
                                }
                            }
                        }
                        
                        // Remove duplicates
                        pagesToConvert = [...new Set(pagesToConvert)];
                        pagesToConvert.sort((a, b) => a - b);
                        
                        // If no valid pages found, convert all
                        if (pagesToConvert.length === 0) {
                            for (let i = 1; i <= totalPages; i++) {
                                pagesToConvert.push(i);
                            }
                        }
                    }
                }
                
                // Reset previous results
                jpgImages = [];
                jpgBlobs = [];
                
                // Convert each page
                const conversionPromises = [];
                
                pagesToConvert.forEach(function(pageNum) {
                    const promise = pdfToJpgDoc.getPage(pageNum).then(function(page) {
                        const viewport = page.getViewport({ scale: scale });
                        
                        // Prepare canvas for rendering
                        const canvas = document.createElement('canvas');
                        const context = canvas.getContext('2d');
                        canvas.height = viewport.height;
                        canvas.width = viewport.width;
                        
                        // Render PDF page on canvas
                        const renderContext = {
                            canvasContext: context,
                            viewport: viewport
                        };
                        
                        return page.render(renderContext).promise.then(function() {
                            // Convert canvas to JPG blob
                            return new Promise(function(resolve) {
                                canvas.toBlob(function(blob) {
                                    resolve({
                                        pageNum: pageNum,
                                        blob: blob,
                                        width: canvas.width,
                                        height: canvas.height
                                    });
                                }, 'image/jpeg', quality);
                            });
                        });
                    });
                    
                    conversionPromises.push(promise);
                });
                
                // Wait for all pages to be converted
                Promise.all(conversionPromises).then(function(results) {
                    // Store results
                    results.forEach(function(result) {
                        jpgBlobs.push(result);
                        
                        // Create image URL for preview (only first image)
                        if (jpgImages.length === 0) {
                            const url = URL.createObjectURL(result.blob);
                            jpgImages.push({
                                url: url,
                                pageNum: result.pageNum
                            });
                            
                            // Show first image in preview
                            jpgResult.innerHTML = '';
                            const img = document.createElement('img');
                            img.src = url;
                            img.alt = `PDF Page ${result.pageNum}`;
                            jpgResult.appendChild(img);
                        }
                    });
                    
                    // Update UI with results
                    jpgCount.textContent = `JPG: ${results.length}`;
                    
                    // Calculate total size
                    let totalSize = 0;
                    results.forEach(function(result) {
                        totalSize += result.blob.size;
                    });
                    jpgTotalSize.textContent = `कुल आकार: ${formatFileSize(totalSize)}`;
                    
                    // Update conversion info
                    pdfToJpgConversionInfo.innerHTML = `
                        <p><strong>कन्वर्जन पूरा!</strong></p>
                        <p>${results.length} पेज JPG में कन्वर्ट हो गए</p>
                        <p>कुल आकार: ${formatFileSize(totalSize)}</p>
                    `;
                    
                    // Enable download buttons
                    downloadAllJpgBtn.disabled = false;
                    downloadSingleJpgBtn.disabled = false;
                    
                    // Remove loading state
                    convertPdfToJpgBtn.classList.remove('loading');
                    convertPdfToJpgBtn.disabled = false;
                    
                }).catch(function(error) {
                    alert('PDF को JPG में कन्वर्ट करने में त्रुटि: ' + error.message);
                    convertPdfToJpgBtn.classList.remove('loading');
                    convertPdfToJpgBtn.disabled = false;
                });
            }
            
            function downloadAllJpgs() {
                if (jpgBlobs.length === 0) return;
                
                // Create a ZIP file containing all JPGs
                const zip = new JSZip();
                
                jpgBlobs.forEach(function(item) {
                    const fileName = `page_${item.pageNum}.jpg`;
                    zip.file(fileName, item.blob);
                });
                
                // Generate ZIP file
                zip.generateAsync({ type: 'blob' }).then(function(content) {
                    // Download ZIP file
                    const link = document.createElement('a');
                    link.href = URL.createObjectURL(content);
                    link.download = `pdf_to_jpg_${pdfToJpgFile.name.replace(/\.[^/.]+$/, "")}.zip`;
                    document.body.appendChild(link);
                    link.click();
                    document.body.removeChild(link);
                });
            }
            
            function downloadFirstJpg() {
                if (jpgBlobs.length === 0) return;
                
                // Download the first JPG
                const firstJpg = jpgBlobs[0];
                const link = document.createElement('a');
                link.href = URL.createObjectURL(firstJpg.blob);
                link.download = `page_${firstJpg.pageNum}.jpg`;
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            }
            
            function resetPdfToJpgAll() {
                // Reset file input
                pdfToJpgFileInput.value = '';
                
                // Reset state variables
                pdfToJpgFile = null;
                pdfToJpgDoc = null;
                jpgImages = [];
                jpgBlobs = [];
                
                // Reset UI
                pdfToJpgPreview.innerHTML = `
                    <i class="fas fa-file-pdf" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                    <p>PDF अपलोड करने पर यहाँ दिखेगा</p>
                `;
                jpgResult.innerHTML = `
                    <i class="fas fa-image" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                    <p>कन्वर्टेड JPG यहाँ दिखेगा</p>
                `;
                
                pdfToJpgFileSize.textContent = 'आकार: --';
                pdfToJpgPageCount.textContent = 'पेज: --';
                jpgCount.textContent = 'JPG: --';
                jpgTotalSize.textContent = 'कुल आकार: --';
                
                // Reset sliders
                jpgQualitySlider.value = 85;
                jpgScaleSlider.value = 1.5;
                jpgQualityValue.textContent = '85';
                jpgScaleValue.textContent = '1.5';
                
                // Reset checkbox and page selector
                convertAllPagesToJpgCheckbox.checked = true;
                pdfToJpgPageSelector.style.display = 'none';
                pdfToJpgPageRange.value = '';
                
                // Reset conversion info
                pdfToJpgConversionInfo.innerHTML = `
                    <p>PDF अपलोड करें और JPG में कन्वर्ट करने के लिए बटन दबाएं</p>
                `;
                
                // Disable buttons
                convertPdfToJpgBtn.disabled = true;
                downloadAllJpgBtn.disabled = true;
                downloadSingleJpgBtn.disabled = true;
            }
            
            // ============================================
            // Utility Functions
            // ============================================
            function formatFileSize(bytes) {
                if (bytes === 0) return '0 Bytes';
                
                const k = 1024;
                const sizes = ['Bytes', 'KB', 'MB'];
                const i = Math.floor(Math.log(bytes) / Math.log(k));
                
                return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
            }
            
            // Initialize all tools
            resetPhotoAll();
            resetPdfAll();
            resetPngToPdf();
            resetPdfToJpgAll();
        });
    </script>
    <amp-auto-ads type="adsense"
            data-ad-client="ca-pub-9474456364191277">
    </amp-auto-ads>
    <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-9474456364191277"
         crossorigin="anonymous"></script>
</body>
</html>
