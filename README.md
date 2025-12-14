<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SUJIT CSC CYBER - फोटो टूल्स</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
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
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
        }
        
        .tab-btn {
            padding: 12px 24px;
            border: none;
            background: none;
            font-size: 1rem;
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
            <h2>SUJIT CSC CYBER - फोटो और PDF टूल्स</h2>
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
                <i class="fas fa-file-pdf"></i> PDF से PNG कन्वर्टर
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
                        <li><a href="#" id="pdfToolLink">PDF से PNG कन्वर्टर</a></li>
                        <li><a href="#features">सुविधाएँ</a></li>
                        <li><a href="#contact">संपर्क</a></li>
                    </ul>
                </div>
                
                <div class="footer-contact">
                    <h3>संपर्क करें</h3>
                    <p><i class="fas fa-map-marker-alt"></i> सीएससी सेंटर, सूरजगंज</p>
                    <p><i class="fas fa-phone"></i> +91 98765 43210</p>
                    <p><i class="fas fa-envelope"></i> info@sujitcsc.com</p>
                </div>
            </div>
            
            <div class="copyright">
                <p>&copy; 2023 SUJIT CSC CYBER. सर्वाधिकार सुरक्षित।</p>
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
            const photoTool = document.getElementById('photoTool');
            const pdfTool = document.getElementById('pdfTool');
            const photoToolLink = document.getElementById('photoToolLink');
            const pdfToolLink = document.getElementById('pdfToolLink');
            
            // Switch to photo tool
            function showPhotoTool() {
                photoTabBtn.classList.add('active');
                pdfTabBtn.classList.remove('active');
                photoTool.classList.add('active');
                pdfTool.classList.remove('active');
            }
            
            // Switch to PDF tool
            function showPdfTool() {
                pdfTabBtn.classList.add('active');
                photoTabBtn.classList.remove('active');
                pdfTool.classList.add('active');
                photoTool.classList.remove('active');
            }
            
            // Event listeners for tabs
            photoTabBtn.addEventListener('click', showPhotoTool);
            pdfTabBtn.addEventListener('click', showPdfTool);
            photoToolLink.addEventListener('click', function(e) {
                e.preventDefault();
                showPhotoTool();
            });
            pdfToolLink.addEventListener('click', function(e) {
                e.preventDefault();
                showPdfTool();
            });
            
            // ============================================
            // Photo Compression Tool (Existing Code)
            // ============================================
            // DOM Elements
            const photoFileInput = document.getElementById('photoFileInput');
            const photoUploadArea = document.getElementById('photoUploadArea');
            const originalImage = document.getElementById('originalImage');
            const compressedImage = document.getElementById('compressedImage');
            const compressBtn = document.getElementById('compressBtn');
            const resetPhotoBtn = document.getElementById('resetPhotoBtn');
            const downloadPhotoBtn = document.getElementById('downloadPhotoBtn');
            const qualitySlider = document.getElementById('quality');
            const widthSlider = document.getElementById('maxWidth');
            const qualityValue = document.getElementById('qualityValue');
            const widthValue = document.getElementById('widthValue');
            const originalSize = document.getElementById('originalSize');
            const originalDimensions = document.getElementById('originalDimensions');
            const compressedSize = document.getElementById('compressedSize');
            const compressedDimensions = document.getElementById('compressedDimensions');
            const sizeReduction = document.getElementById('sizeReduction');
            const compressionRatio = document.getElementById('compressionRatio');
            
            // State variables
            let originalFile = null;
            let originalImageData = null;
            let compressedImageData = null;
            let compressedBlob = null;
            
            // Event Listeners for photo tool
            photoUploadArea.addEventListener('click', () => photoFileInput.click());
            photoUploadArea.addEventListener('dragover', (e) => {
                e.preventDefault();
                photoUploadArea.style.borderColor = '#3498db';
                photoUploadArea.style.backgroundColor = 'rgba(52, 152, 219, 0.1)';
            });
            photoUploadArea.addEventListener('dragleave', () => {
                photoUploadArea.style.borderColor = '#ecf0f1';
                photoUploadArea.style.backgroundColor = 'transparent';
            });
            photoUploadArea.addEventListener('drop', (e) => {
                e.preventDefault();
                photoUploadArea.style.borderColor = '#ecf0f1';
                photoUploadArea.style.backgroundColor = 'transparent';
                
                if (e.dataTransfer.files.length) {
                    handlePhotoFileSelect(e.dataTransfer.files[0]);
                }
            });
            
            photoFileInput.addEventListener('change', (e) => {
                if (e.target.files.length) {
                    handlePhotoFileSelect(e.target.files[0]);
                }
            });
            
            qualitySlider.addEventListener('input', () => {
                qualityValue.textContent = qualitySlider.value;
            });
            
            widthSlider.addEventListener('input', () => {
                widthValue.textContent = widthSlider.value;
            });
            
            compressBtn.addEventListener('click', compressImage);
            resetPhotoBtn.addEventListener('click', resetPhotoAll);
            downloadPhotoBtn.addEventListener('click', downloadCompressedImage);
            
            // Functions for photo tool
            function handlePhotoFileSelect(file) {
                // Check if file is an image
                if (!file.type.match('image.*')) {
                    alert('कृपया केवल इमेज फाइल अपलोड करें (JPG, PNG, WebP)।');
                    return;
                }
                
                // Check file size (5MB limit)
                if (file.size > 5 * 1024 * 1024) {
                    alert('फाइल का आकार 5MB से कम होना चाहिए।');
                    return;
                }
                
                originalFile = file;
                
                // Display original file info
                originalSize.textContent = `आकार: ${formatFileSize(file.size)}`;
                
                // Display original image
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = new Image();
                    img.onload = function() {
                        originalDimensions.textContent = `डाइमेंशन: ${img.width} × ${img.height}`;
                        originalImage.innerHTML = '';
                        originalImage.appendChild(img);
                        
                        // Store original image data
                        originalImageData = {
                            src: e.target.result,
                            width: img.width,
                            height: img.height,
                            size: file.size
                        };
                        
                        // Enable compress button
                        compressBtn.disabled = false;
                    };
                    img.src = e.target.result;
                };
                reader.readAsDataURL(file);
            }
            
            function compressImage() {
                if (!originalFile) {
                    alert('कृपया पहले एक फोटो अपलोड करें।');
                    return;
                }
                
                // Show loading state
                compressBtn.classList.add('loading');
                compressBtn.disabled = true;
                
                // Get compression settings
                const quality = parseInt(qualitySlider.value) / 100;
                const maxWidth = parseInt(widthSlider.value);
                
                // Create an image element with the original file
                const img = new Image();
                img.onload = function() {
                    // Calculate new dimensions while maintaining aspect ratio
                    let width = img.width;
                    let height = img.height;
                    
                    if (width > maxWidth) {
                        height = Math.round((height * maxWidth) / width);
                        width = maxWidth;
                    }
                    
                    // Create canvas for compression
                    const canvas = document.createElement('canvas');
                    canvas.width = width;
                    canvas.height = height;
                    
                    // Draw image on canvas with new dimensions
                    const ctx = canvas.getContext('2d');
                    ctx.drawImage(img, 0, 0, width, height);
                    
                    // Compress image
                    canvas.toBlob(function(blob) {
                        // Display compressed image
                        const compressedUrl = URL.createObjectURL(blob);
                        const compressedImg = new Image();
                        compressedImg.onload = function() {
                            compressedImage.innerHTML = '';
                            compressedImage.appendChild(compressedImg);
                            
                            // Update compressed image info
                            compressedSize.textContent = `आकार: ${formatFileSize(blob.size)}`;
                            compressedDimensions.textContent = `डाइमेंशन: ${width} × ${height}`;
                            
                            // Calculate and display compression stats
                            const originalSizeBytes = originalFile.size;
                            const compressedSizeBytes = blob.size;
                            const reduction = originalSizeBytes - compressedSizeBytes;
                            const reductionPercent = ((reduction / originalSizeBytes) * 100).toFixed(1);
                            const ratio = (originalSizeBytes / compressedSizeBytes).toFixed(1);
                            
                            sizeReduction.textContent = `${reductionPercent}%`;
                            compressionRatio.textContent = `${ratio}:1`;
                            
                            // Store compressed data for download
                            compressedBlob = blob;
                            compressedImageData = {
                                url: compressedUrl,
                                width: width,
                                height: height,
                                size: compressedSizeBytes
                            };
                            
                            // Enable download button
                            downloadPhotoBtn.disabled = false;
                            
                            // Remove loading state
                            compressBtn.classList.remove('loading');
                            compressBtn.disabled = false;
                        };
                        compressedImg.src = compressedUrl;
                        
                    }, 'image/jpeg', quality);
                };
                
                img.src = URL.createObjectURL(originalFile);
            }
            
            function downloadCompressedImage() {
                if (!compressedBlob) return;
                
                const link = document.createElement('a');
                link.href = URL.createObjectURL(compressedBlob);
                link.download = `compressed_${originalFile.name.replace(/\.[^/.]+$/, "")}.jpg`;
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            }
            
            function resetPhotoAll() {
                // Reset file input
                photoFileInput.value = '';
                
                // Reset state variables
                originalFile = null;
                originalImageData = null;
                compressedImageData = null;
                compressedBlob = null;
                
                // Reset UI
                originalImage.innerHTML = `
                    <i class="fas fa-image" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                    <p>फोटो अपलोड करने पर यहाँ दिखेगा</p>
                `;
                compressedImage.innerHTML = `
                    <i class="fas fa-file-archive" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                    <p>कम्प्रेस्ड फोटो यहाँ दिखेगा</p>
                `;
                
                originalSize.textContent = 'आकार: --';
                originalDimensions.textContent = 'डाइमेंशन: --';
                compressedSize.textContent = 'आकार: --';
                compressedDimensions.textContent = 'डाइमेंशन: --';
                sizeReduction.textContent = '--';
                compressionRatio.textContent = '--';
                
                // Reset sliders
                qualitySlider.value = 70;
                widthSlider.value = 1200;
                qualityValue.textContent = '70';
                widthValue.textContent = '1200';
                
                // Disable buttons
                compressBtn.disabled = true;
                downloadPhotoBtn.disabled = true;
            }
            
            // ============================================
            // PDF to PNG Converter Tool (New Code)
            // ============================================
            // DOM Elements for PDF tool
            const pdfFileInput = document.getElementById('pdfFileInput');
            const pdfUploadArea = document.getElementById('pdfUploadArea');
            const pdfPreview = document.getElementById('pdfPreview');
            const pngResult = document.getElementById('pngResult');
            const convertPdfBtn = document.getElementById('convertPdfBtn');
            const resetPdfBtn = document.getElementById('resetPdfBtn');
            const downloadAllBtn = document.getElementById('downloadAllBtn');
            const downloadSingleBtn = document.getElementById('downloadSingleBtn');
            const pdfQualitySlider = document.getElementById('pdfQuality');
            const pdfScaleSlider = document.getElementById('pdfScale');
            const pdfQualityValue = document.getElementById('pdfQualityValue');
            const pdfScaleValue = document.getElementById('pdfScaleValue');
            const pdfFileSize = document.getElementById('pdfFileSize');
            const pdfPageCount = document.getElementById('pdfPageCount');
            const pngCount = document.getElementById('pngCount');
            const pngTotalSize = document.getElementById('pngTotalSize');
            const conversionInfo = document.getElementById('conversionInfo');
            const convertAllPagesCheckbox = document.getElementById('convertAllPages');
            const pageSelector = document.getElementById('pageSelector');
            const pageRangeInput = document.getElementById('pageRange');
            
            // State variables for PDF tool
            let pdfFile = null;
            let pdfDoc = null;
            let pngImages = [];
            let pngBlobs = [];
            
            // Event Listeners for PDF tool
            pdfUploadArea.addEventListener('click', () => pdfFileInput.click());
            pdfUploadArea.addEventListener('dragover', (e) => {
                e.preventDefault();
                pdfUploadArea.style.borderColor = '#3498db';
                pdfUploadArea.style.backgroundColor = 'rgba(52, 152, 219, 0.1)';
            });
            pdfUploadArea.addEventListener('dragleave', () => {
                pdfUploadArea.style.borderColor = '#ecf0f1';
                pdfUploadArea.style.backgroundColor = 'transparent';
            });
            pdfUploadArea.addEventListener('drop', (e) => {
                e.preventDefault();
                pdfUploadArea.style.borderColor = '#ecf0f1';
                pdfUploadArea.style.backgroundColor = 'transparent';
                
                if (e.dataTransfer.files.length) {
                    handlePdfFileSelect(e.dataTransfer.files[0]);
                }
            });
            
            pdfFileInput.addEventListener('change', (e) => {
                if (e.target.files.length) {
                    handlePdfFileSelect(e.target.files[0]);
                }
            });
            
            pdfQualitySlider.addEventListener('input', () => {
                pdfQualityValue.textContent = pdfQualitySlider.value;
            });
            
            pdfScaleSlider.addEventListener('input', () => {
                pdfScaleValue.textContent = pdfScaleSlider.value;
            });
            
            convertPdfBtn.addEventListener('click', convertPdfToPng);
            resetPdfBtn.addEventListener('click', resetPdfAll);
            downloadAllBtn.addEventListener('click', downloadAllPngs);
            downloadSingleBtn.addEventListener('click', downloadFirstPng);
            
            convertAllPagesCheckbox.addEventListener('change', function() {
                if (this.checked) {
                    pageSelector.style.display = 'none';
                } else {
                    pageSelector.style.display = 'block';
                }
            });
            
            // Functions for PDF tool
            function handlePdfFileSelect(file) {
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
                
                pdfFile = file;
                
                // Display file info
                pdfFileSize.textContent = `आकार: ${formatFileSize(file.size)}`;
                
                // Load PDF for preview
                const reader = new FileReader();
                reader.onload = function(e) {
                    const typedarray = new Uint8Array(e.target.result);
                    
                    // Load PDF document
                    pdfjsLib.getDocument(typedarray).promise.then(function(doc) {
                        pdfDoc = doc;
                        const numPages = doc.numPages;
                        pdfPageCount.textContent = `पेज: ${numPages}`;
                        
                        // Update conversion info
                        conversionInfo.innerHTML = `
                            <p><strong>PDF लोड हो गया!</strong></p>
                            <p>कुल पेज: ${numPages}</p>
                            <p>PNG में कन्वर्ट करने के लिए बटन दबाएं</p>
                        `;
                        
                        // Show first page as preview
                        renderPagePreview(1);
                        
                        // Enable convert button
                        convertPdfBtn.disabled = false;
                    }).catch(function(error) {
                        alert('PDF लोड करने में त्रुटि: ' + error.message);
                    });
                };
                reader.readAsArrayBuffer(file);
            }
            
            function renderPagePreview(pageNum) {
                if (!pdfDoc) return;
                
                pdfDoc.getPage(pageNum).then(function(page) {
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
                        pdfPreview.innerHTML = '';
                        canvas.classList.add('pdf-page-preview');
                        pdfPreview.appendChild(canvas);
                        
                        // Add page info
                        const pageInfo = document.createElement('p');
                        pageInfo.textContent = `पेज ${pageNum} / ${pdfDoc.numPages}`;
                        pageInfo.style.marginTop = '10px';
                        pageInfo.style.fontSize = '0.9rem';
                        pdfPreview.appendChild(pageInfo);
                    });
                });
            }
            
            function convertPdfToPng() {
                if (!pdfDoc) {
                    alert('कृपया पहले एक PDF अपलोड करें।');
                    return;
                }
                
                // Show loading state
                convertPdfBtn.classList.add('loading');
                convertPdfBtn.disabled = true;
                
                // Get conversion settings
                const quality = parseInt(pdfQualitySlider.value) / 100;
                const scale = parseFloat(pdfScaleSlider.value);
                
                // Determine which pages to convert
                let pagesToConvert = [];
                const totalPages = pdfDoc.numPages;
                
                if (convertAllPagesCheckbox.checked) {
                    // Convert all pages
                    for (let i = 1; i <= totalPages; i++) {
                        pagesToConvert.push(i);
                    }
                } else {
                    // Parse page range input
                    const pageRange = pageRangeInput.value.trim();
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
                pngImages = [];
                pngBlobs = [];
                
                // Convert each page
                const conversionPromises = [];
                
                pagesToConvert.forEach(function(pageNum) {
                    const promise = pdfDoc.getPage(pageNum).then(function(page) {
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
                            // Convert canvas to PNG blob
                            return new Promise(function(resolve) {
                                canvas.toBlob(function(blob) {
                                    resolve({
                                        pageNum: pageNum,
                                        blob: blob,
                                        width: canvas.width,
                                        height: canvas.height
                                    });
                                }, 'image/png', quality);
                            });
                        });
                    });
                    
                    conversionPromises.push(promise);
                });
                
                // Wait for all pages to be converted
                Promise.all(conversionPromises).then(function(results) {
                    // Store results
                    results.forEach(function(result) {
                        pngBlobs.push(result);
                        
                        // Create image URL for preview (only first image)
                        if (pngImages.length === 0) {
                            const url = URL.createObjectURL(result.blob);
                            pngImages.push({
                                url: url,
                                pageNum: result.pageNum
                            });
                            
                            // Show first image in preview
                            pngResult.innerHTML = '';
                            const img = document.createElement('img');
                            img.src = url;
                            img.alt = `PDF Page ${result.pageNum}`;
                            pngResult.appendChild(img);
                        }
                    });
                    
                    // Update UI with results
                    pngCount.textContent = `PNG: ${results.length}`;
                    
                    // Calculate total size
                    let totalSize = 0;
                    results.forEach(function(result) {
                        totalSize += result.blob.size;
                    });
                    pngTotalSize.textContent = `कुल आकार: ${formatFileSize(totalSize)}`;
                    
                    // Update conversion info
                    conversionInfo.innerHTML = `
                        <p><strong>कन्वर्जन पूरा!</strong></p>
                        <p>${results.length} पेज PNG में कन्वर्ट हो गए</p>
                        <p>कुल आकार: ${formatFileSize(totalSize)}</p>
                    `;
                    
                    // Enable download buttons
                    downloadAllBtn.disabled = false;
                    downloadSingleBtn.disabled = false;
                    
                    // Remove loading state
                    convertPdfBtn.classList.remove('loading');
                    convertPdfBtn.disabled = false;
                    
                }).catch(function(error) {
                    alert('PDF को PNG में कन्वर्ट करने में त्रुटि: ' + error.message);
                    convertPdfBtn.classList.remove('loading');
                    convertPdfBtn.disabled = false;
                });
            }
            
            function downloadAllPngs() {
                if (pngBlobs.length === 0) return;
                
                // Create a ZIP file containing all PNGs
                const zip = new JSZip();
                
                pngBlobs.forEach(function(item) {
                    const fileName = `page_${item.pageNum}.png`;
                    zip.file(fileName, item.blob);
                });
                
                // Generate ZIP file
                zip.generateAsync({ type: 'blob' }).then(function(content) {
                    // Download ZIP file
                    const link = document.createElement('a');
                    link.href = URL.createObjectURL(content);
                    link.download = `pdf_converted_${pdfFile.name.replace(/\.[^/.]+$/, "")}.zip`;
                    document.body.appendChild(link);
                    link.click();
                    document.body.removeChild(link);
                });
            }
            
            function downloadFirstPng() {
                if (pngBlobs.length === 0) return;
                
                // Download the first PNG
                const firstPng = pngBlobs[0];
                const link = document.createElement('a');
                link.href = URL.createObjectURL(firstPng.blob);
                link.download = `page_${firstPng.pageNum}.png`;
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            }
            
            function resetPdfAll() {
                // Reset file input
                pdfFileInput.value = '';
                
                // Reset state variables
                pdfFile = null;
                pdfDoc = null;
                pngImages = [];
                pngBlobs = [];
                
                // Reset UI
                pdfPreview.innerHTML = `
                    <i class="fas fa-file-pdf" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                    <p>PDF अपलोड करने पर यहाँ दिखेगा</p>
                `;
                pngResult.innerHTML = `
                    <i class="fas fa-image" style="font-size: 3rem; margin-bottom: 1rem;"></i>
                    <p>कन्वर्टेड PNG यहाँ दिखेगा</p>
                `;
                
                pdfFileSize.textContent = 'आकार: --';
                pdfPageCount.textContent = 'पेज: --';
                pngCount.textContent = 'PNG: --';
                pngTotalSize.textContent = 'कुल आकार: --';
                
                // Reset sliders
                pdfQualitySlider.value = 90;
                pdfScaleSlider.value = 2;
                pdfQualityValue.textContent = '90';
                pdfScaleValue.textContent = '2.0';
                
                // Reset checkbox and page selector
                convertAllPagesCheckbox.checked = true;
                pageSelector.style.display = 'none';
                pageRangeInput.value = '';
                
                // Reset conversion info
                conversionInfo.innerHTML = `
                    <p>PDF अपलोड करें और PNG में कन्वर्ट करने के लिए बटन दबाएं</p>
                `;
                
                // Disable buttons
                convertPdfBtn.disabled = true;
                downloadAllBtn.disabled = true;
                downloadSingleBtn.disabled = true;
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
            
            // Initialize the app
            resetPhotoAll();
            resetPdfAll();
        });
    </script>
</body>
</html>
