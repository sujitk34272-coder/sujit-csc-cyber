<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>फोटो टूल्स | Image Resizer, Converter & Background Remover</title>
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
            --purple-color: #9b59b6;
            --orange-color: #e67e22;
            --pink-color: #e84393;
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
            flex-wrap: wrap;
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
            flex-wrap: wrap;
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
        }
        
        .hero p {
            font-size: 1.2rem;
            max-width: 700px;
            margin: 0 auto;
        }
        
        .tool-tabs {
            display: flex;
            justify-content: center;
            margin-bottom: 2rem;
            background-color: white;
            border-radius: 15px;
            padding: 0.5rem;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            max-width: 1200px;
            margin-left: auto;
            margin-right: auto;
            flex-wrap: wrap;
            gap: 5px;
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
        }
        
        .tab-btn:hover {
            background-color: rgba(52, 152, 219, 0.1);
        }
        
        .tab-btn.active {
            background-color: var(--secondary-color);
            color: white;
        }
        
        .tool-container {
            display: none;
        }
        
        .tool-container.active {
            display: block;
        }
        
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
            .tab-btn {
                padding: 8px 12px;
                font-size: 0.7rem;
            }
        }
        
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
        
        .dimension-inputs {
            display: flex;
            gap: 15px;
            align-items: center;
            flex-wrap: wrap;
        }
        
        .dimension-inputs input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
            text-align: center;
        }
        
        .dimension-inputs span {
            font-weight: bold;
            color: var(--dark-color);
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
        
        .buttons {
            display: flex;
            gap: 15px;
            margin-top: 2rem;
            flex-wrap: wrap;
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
            transform: translateY(-2px);
        }
        
        .btn-secondary {
            background-color: var(--light-color);
            color: var(--dark-color);
        }
        
        .btn-secondary:hover {
            background-color: #d5dbdb;
            transform: translateY(-2px);
        }
        
        .btn-success {
            background-color: var(--success-color);
            color: white;
        }
        
        .btn-orange {
            background-color: var(--orange-color);
            color: white;
        }
        
        .btn-purple {
            background-color: var(--purple-color);
            color: white;
        }
        
        .btn-pink {
            background-color: var(--pink-color);
            color: white;
        }
        
        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }
        
        .preview-section {
            background-color: white;
            border-radius: 15px;
            padding: 2rem;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
        }
        
        .image-placeholder {
            width: 100%;
            min-height: 200px;
            background-color: var(--light-color);
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: #777;
            overflow: hidden;
            padding: 1rem;
        }
        
        .image-placeholder img {
            max-width: 100%;
            max-height: 250px;
            object-fit: contain;
        }
        
        .image-info {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            font-size: 0.9rem;
            color: #666;
            flex-wrap: wrap;
            gap: 8px;
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
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--secondary-color);
            margin-bottom: 5px;
        }
        
        .compression-stats {
            background-color: #f8f9fa;
            border-radius: 10px;
            padding: 1.5rem;
            margin-top: 2rem;
        }
        
        .preset-buttons {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
            gap: 8px;
            margin-top: 10px;
        }
        
        .preset-btn {
            padding: 6px 10px;
            background-color: var(--light-color);
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.75rem;
            transition: all 0.2s;
        }
        
        .preset-btn:hover {
            background-color: var(--secondary-color);
            color: white;
        }
        
        .aspect-ratio-badge {
            font-size: 0.8rem;
            color: #666;
            margin-top: 5px;
            padding: 5px;
            background: #f8f9fa;
            border-radius: 5px;
            text-align: center;
        }
        
        .kb-slider-container {
            margin-top: 15px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 10px;
        }
        
        .target-size-display {
            font-size: 1rem;
            font-weight: bold;
            color: var(--orange-color);
            text-align: center;
            margin-top: 10px;
        }
        
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
        }
        
        .feature-icon {
            font-size: 2.5rem;
            color: var(--secondary-color);
            margin-bottom: 1.5rem;
        }
        
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
        
        .loading {
            opacity: 0.6;
            pointer-events: none;
        }
        
        select, input[type="number"] {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 1rem;
        }
        
        .info-text {
            font-size: 0.75rem;
            color: #666;
            margin-top: 5px;
        }
        
        .pdf-preview-container {
            width: 100%;
            min-height: 200px;
            background-color: var(--light-color);
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }
        
        .bg-remove-badge {
            background: #f1f9ff;
            border-radius: 8px;
            padding: 8px;
            font-size: 0.8rem;
            margin-top: 10px;
            text-align: center;
        }
        
        .alert-message {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #333;
            color: white;
            padding: 12px 20px;
            border-radius: 8px;
            z-index: 9999;
            animation: slideIn 0.3s ease;
        }
        
        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container header-container">
            <div class="logo">
                <div class="logo-icon"><i class="fas fa-tools"></i></div>
                <h1>SUJIT <span>CSC CYBER</span></h1>
            </div>
            <nav>
                <ul>
                    <li><a href="#home">होम</a></li>
                    <li><a href="#features">सुविधाएँ</a></li>
                    <li><a href="#contact">संपर्क</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <section class="hero" id="home">
        <div class="container">
            <h2>फोटो और PDF टूल्स</h2>
            <p>आपकी तस्वीरों और PDF फाइलों के लिए सर्वोत्तम टूल्स। तेज़, सुरक्षित और मुफ्त सेवाएं। अब बैकग्राउंड हटाएं!</p>
        </div>
    </section>

    <div class="container">
        <div class="tool-tabs">
            <button class="tab-btn active" id="photoTabBtn"><i class="fas fa-compress-alt"></i> फोटो कॉम्प्रेसर</button>
            <button class="tab-btn" id="resizeTabBtn"><i class="fas fa-expand-alt"></i> इमेज रिसाइज़र</button>
            <button class="tab-btn" id="pdfTabBtn"><i class="fas fa-file-pdf"></i> PDF से PNG</button>
            <button class="tab-btn" id="pngToPdfTabBtn"><i class="fas fa-file-image"></i> PNG से PDF</button>
            <button class="tab-btn" id="bgRemoveTabBtn"><i class="fas fa-magic"></i> Remove BG</button>
        </div>
    </div>

    <!-- Photo Compressor Tool -->
    <div class="container">
        <div class="tool-container active" id="photoTool">
            <div class="main-content">
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-cloud-upload-alt"></i> फोटो अपलोड करें</h2>
                    <div class="upload-area" id="photoUploadArea">
                        <i class="fas fa-file-image"></i>
                        <p>क्लिक करें या फोटो यहाँ खींचें</p>
                        <span>JPG, PNG, WebP (अधिकतम 5MB)</span>
                        <input type="file" id="photoFileInput" class="fileInput" accept="image/*">
                    </div>
                    <div class="controls">
                        <div class="control-group">
                            <label>क्वालिटी: <span id="qualityValue">70</span>%</label>
                            <div class="slider-container">
                                <span>0</span>
                                <input type="range" id="quality" min="0" max="100" value="70">
                                <span>100</span>
                            </div>
                        </div>
                        <div class="control-group">
                            <label>अधिकतम चौड़ाई: <span id="widthValue">1200</span>px</label>
                            <div class="slider-container">
                                <span>300</span>
                                <input type="range" id="maxWidth" min="300" max="2000" value="1200">
                                <span>2000</span>
                            </div>
                        </div>
                    </div>
                    <div class="buttons">
                        <button class="btn btn-primary" id="compressBtn"><i class="fas fa-compress-alt"></i> कॉम्प्रेस करें</button>
                        <button class="btn btn-secondary" id="resetPhotoBtn"><i class="fas fa-redo"></i> रीसेट</button>
                    </div>
                </section>
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> प्रीव्यू</h2>
                    <div class="image-placeholder" id="originalImage"><i class="fas fa-image" style="font-size: 3rem;"></i><p>मूल फोटो</p></div>
                    <div class="image-info"><span id="originalSize">आकार: --</span><span id="originalDimensions">डाइमेंशन: --</span></div>
                    <div class="image-placeholder" id="compressedImage" style="margin-top: 20px;"><i class="fas fa-file-archive" style="font-size: 3rem;"></i><p>कम्प्रेस्ड फोटो</p></div>
                    <div class="image-info"><span id="compressedSize">आकार: --</span><span id="compressedDimensions">डाइमेंशन: --</span></div>
                    <div class="compression-stats">
                        <div class="stats-grid">
                            <div class="stat-item"><div class="stat-value" id="sizeReduction">--</div><div class="stat-label">आकार कमी</div></div>
                            <div class="stat-item"><div class="stat-value" id="compressionRatio">--</div><div class="stat-label">अनुपात</div></div>
                        </div>
                        <button class="btn btn-success" id="downloadPhotoBtn" disabled><i class="fas fa-download"></i> डाउनलोड करें</button>
                    </div>
                </section>
            </div>
        </div>

        <!-- Image Resizer Tool - FIXED -->
        <div class="tool-container" id="resizeTool">
            <div class="main-content">
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-expand-alt"></i> इमेज रिसाइज़ करें</h2>
                    <div class="upload-area" id="resizeUploadArea">
                        <i class="fas fa-file-image"></i>
                        <p>क्लिक करें या इमेज यहाँ खींचें</p>
                        <span>JPG, PNG, WebP (अधिकतम 10MB)</span>
                        <input type="file" id="resizeFileInput" class="fileInput" accept="image/*">
                    </div>
                    <div class="controls">
                        <div class="control-group">
                            <label><i class="fas fa-arrows-alt"></i> नए डाइमेंशन (पिक्सेल में)</label>
                            <div class="dimension-inputs">
                                <input type="number" id="resizeWidth" placeholder="चौड़ाई" value="800" step="10">
                                <span>×</span>
                                <input type="number" id="resizeHeight" placeholder="ऊंचाई" value="600" step="10">
                            </div>
                            <div class="aspect-ratio-badge" id="aspectRatioDisplay">मूल अनुपात: --</div>
                        </div>
                        
                        <div class="checkbox-group">
                            <input type="checkbox" id="maintainAspectRatio" checked>
                            <label for="maintainAspectRatio">अनुपात बनाए रखें</label>
                        </div>
                        
                        <div class="control-group">
                            <label><i class="fas fa-chart-line"></i> प्रीसेट साइज़ (KB में)</label>
                            <div class="preset-buttons">
                                <button class="preset-btn" data-kb="10">10 KB</button>
                                <button class="preset-btn" data-kb="50">50 KB</button>
                                <button class="preset-btn" data-kb="100">100 KB</button>
                                <button class="preset-btn" data-kb="200">200 KB</button>
                                <button class="preset-btn" data-kb="300">300 KB</button>
                                <button class="preset-btn" data-kb="500">500 KB</button>
                                <button class="preset-btn" data-kb="800">800 KB</button>
                                <button class="preset-btn" data-kb="1000">1000 KB (1MB)</button>
                            </div>
                        </div>
                        
                        <div class="kb-slider-container">
                            <label>या स्लाइडर से चुनें (10KB - 1000KB)</label>
                            <div class="slider-container">
                                <span>10KB</span>
                                <input type="range" id="kbTargetSlider" min="10" max="1000" value="200" step="5">
                                <span>1000KB</span>
                            </div>
                            <div class="target-size-display" id="targetSizeDisplay">लक्ष्य आकार: 200 KB</div>
                        </div>
                        
                        <div class="control-group">
                            <label for="outputFormatResize">आउटपुट फॉर्मेट:</label>
                            <select id="outputFormatResize">
                                <option value="image/jpeg">JPEG (सबसे छोटा)</option>
                                <option value="image/webp">WebP (बेहतर कम्प्रेशन)</option>
                                <option value="image/png">PNG (लॉसलेस)</option>
                            </select>
                        </div>
                    </div>
                    <div class="buttons">
                        <button class="btn btn-orange" id="resizeBtn"><i class="fas fa-expand-alt"></i> डाइमेंशन से रिसाइज़ करें</button>
                        <button class="btn btn-purple" id="resizeByKbBtn"><i class="fas fa-chart-line"></i> KB साइज़ से रिसाइज़ करें</button>
                        <button class="btn btn-secondary" id="resetResizeBtn"><i class="fas fa-redo"></i> रीसेट</button>
                    </div>
                </section>
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> प्रीव्यू और डाउनलोड</h2>
                    <div class="image-placeholder" id="originalResizeImage"><i class="fas fa-image" style="font-size: 3rem;"></i><p>मूल इमेज</p></div>
                    <div class="image-info"><span id="originalResizeSize">आकार: --</span><span id="originalResizeDimensions">डाइमेंशन: --</span></div>
                    <div class="image-placeholder" id="resizedImage" style="margin-top: 20px;"><i class="fas fa-expand-alt" style="font-size: 3rem;"></i><p>रिसाइज़ की गई इमेज</p></div>
                    <div class="image-info"><span id="resizedSize">आकार: --</span><span id="resizedDimensions">डाइमेंशन: --</span></div>
                    <div class="compression-stats">
                        <div class="stats-grid">
                            <div class="stat-item"><div class="stat-value" id="resizeChange">--</div><div class="stat-label">आकार परिवर्तन</div></div>
                            <div class="stat-item"><div class="stat-value" id="targetAchieved">--</div><div class="stat-label">लक्ष्य से तुलना</div></div>
                        </div>
                        <button class="btn btn-success" id="downloadResizeBtn" disabled><i class="fas fa-download"></i> रिसाइज़्ड इमेज डाउनलोड करें</button>
                    </div>
                </section>
            </div>
        </div>

        <!-- PDF to PNG Tool - FIXED -->
        <div class="tool-container" id="pdfTool">
            <div class="main-content">
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-file-upload"></i> PDF अपलोड करें</h2>
                    <div class="upload-area" id="pdfUploadArea"><i class="fas fa-file-pdf"></i><p>क्लिक करें या PDF यहाँ खींचें</p><input type="file" id="pdfFileInput" class="fileInput" accept=".pdf"></div>
                    <div class="buttons">
                        <button class="btn btn-primary" id="convertPdfBtn"><i class="fas fa-sync-alt"></i> PNG में बदलें</button>
                        <button class="btn btn-secondary" id="resetPdfBtn">रीसेट</button>
                    </div>
                </section>
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> प्रीव्यू</h2>
                    <div class="pdf-preview-container" id="pdfPreview"><i class="fas fa-file-pdf" style="font-size: 3rem;"></i><p>PDF प्रीव्यू</p></div>
                    <div class="image-info" id="pdfInfo" style="display: none;"><span id="pdfPageCount"></span></div>
                    <button class="btn btn-success" id="downloadPdfResultBtn" disabled style="margin-top: 15px;"><i class="fas fa-download"></i> PNG डाउनलोड करें</button>
                </section>
            </div>
        </div>

        <!-- PNG to PDF Tool -->
        <div class="tool-container" id="pngToPdfTool">
            <div class="main-content">
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-images"></i> Images अपलोड करें</h2>
                    <div class="upload-area" id="pngUploadArea"><i class="fas fa-file-image"></i><p>क्लिक करें या इमेज यहाँ खींचें</p><span>एक या अधिक इमेज</span><input type="file" id="pngFileInput" class="fileInput" accept="image/*" multiple></div>
                    <div class="buttons">
                        <button class="btn btn-purple" id="convertToPdfBtn"><i class="fas fa-file-pdf"></i> PDF बनाएँ</button>
                        <button class="btn btn-secondary" id="resetPngToPdfBtn">रीसेट</button>
                    </div>
                </section>
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> प्रीव्यू</h2>
                    <div class="image-placeholder" id="pngPreviewArea"><i class="fas fa-images"></i><p>इमेज प्रीव्यू</p></div>
                    <div class="image-info"><span id="imageCount">इमेज: 0</span></div>
                    <button class="btn btn-success" id="downloadPdfBtn2" disabled style="margin-top: 15px;"><i class="fas fa-download"></i> PDF डाउनलोड करें</button>
                </section>
            </div>
        </div>

        <!-- REMOVE BACKGROUND TOOL - FIXED -->
        <div class="tool-container" id="bgRemoveTool">
            <div class="main-content">
                <section class="upload-section">
                    <h2 class="section-title"><i class="fas fa-magic"></i> बैकग्राउंड हटाएँ</h2>
                    <div class="upload-area" id="bgUploadArea">
                        <i class="fas fa-user-circle"></i>
                        <p>क्लिक करें या फोटो यहाँ खींचें (पोर्ट्रेट/ऑब्जेक्ट)</p>
                        <span>JPG, PNG, WebP (Max 8MB)</span>
                        <input type="file" id="bgFileInput" class="fileInput" accept="image/*">
                    </div>
                    <div class="controls">
                        <div class="control-group">
                            <label><i class="fas fa-palette"></i> पारदर्शिता / बैकग्राउंड रंग</label>
                            <select id="bgOutputType">
                                <option value="transparent">पारदर्शी (PNG)</option>
                                <option value="white">सफेद बैकग्राउंड</option>
                                <option value="custom">कस्टम रंग</option>
                            </select>
                            <input type="color" id="customBgColor" value="#ffffff" style="margin-top: 8px; width: 100%;">
                        </div>
                        <div class="control-group">
                            <label><i class="fas fa-sliders-h"></i> एज स्मूथिंग (धार)</label>
                            <div class="slider-container">
                                <span>0</span>
                                <input type="range" id="edgeSmoothing" min="0" max="100" value="70">
                                <span>100</span>
                            </div>
                        </div>
                        <div class="info-text bg-remove-badge">
                            <i class="fas fa-info-circle"></i> स्मार्ट एल्गोरिदम: मुख्य विषय को पहचान कर बैकग्राउंड हटाता है। बेहतर परिणाम के लिए साफ़ बैकग्राउंड वाली फोटो अपलोड करें।
                        </div>
                    </div>
                    <div class="buttons">
                        <button class="btn btn-pink" id="removeBgBtn"><i class="fas fa-cut"></i> बैकग्राउंड हटाएँ</button>
                        <button class="btn btn-secondary" id="resetBgBtn"><i class="fas fa-redo"></i> रीसेट</button>
                    </div>
                </section>
                <section class="preview-section">
                    <h2 class="section-title"><i class="fas fa-eye"></i> प्रीव्यू और डाउनलोड</h2>
                    <div class="image-placeholder" id="originalBgImage"><i class="fas fa-image" style="font-size: 3rem;"></i><p>मूल इमेज</p></div>
                    <div class="image-info"><span id="originalBgSize">आकार: --</span><span id="originalBgDimensions">डाइमेंशन: --</span></div>
                    <div class="image-placeholder" id="removedBgImage" style="margin-top: 20px; background: repeating-linear-gradient(45deg, #ddd, #ddd 10px, #eee 10px, #eee 20px);"><i class="fas fa-sticky-note" style="font-size: 3rem;"></i><p>हटाया गया बैकग्राउंड</p></div>
                    <div class="image-info"><span id="removedBgSize">आकार: --</span><span id="removedBgDimensions">डाइमेंशन: --</span></div>
                    <div class="compression-stats">
                        <button class="btn btn-success" id="downloadBgBtn" disabled><i class="fas fa-download"></i> PNG (बिना BG) डाउनलोड करें</button>
                    </div>
                </section>
            </div>
        </div>
        
        <section class="features" id="features">
            <h2>हमारी विशेषताएँ</h2>
            <div class="features-grid">
                <div class="feature-card"><div class="feature-icon"><i class="fas fa-bolt"></i></div><h3>तेज़ प्रोसेसिंग</h3><p>सेकंडों में रिजल्ट</p></div>
                <div class="feature-card"><div class="feature-icon"><i class="fas fa-shield-alt"></i></div><h3>100% सुरक्षित</h3><p>सर्वर पर स्टोर नहीं</p></div>
                <div class="feature-card"><div class="feature-icon"><i class="fas fa-chart-line"></i></div><h3>KB प्रीसेट</h3><p>10KB से 1000KB तक</p></div>
                <div class="feature-card"><div class="feature-icon"><i class="fas fa-magic"></i></div><h3>बैकग्राउंड हटाएँ</h3><p>AI-आधारित रिमूवल</p></div>
            </div>
        </section>
    </div>

    <footer id="contact">
        <div class="container">
            <div class="footer-container">
                <div class="footer-logo"><h2>SUJIT <span>CSC CYBER</span></h2><p>आपकी फोटो और PDF के लिए</p></div>
                <div class="footer-links"><h3>टूल्स</h3><ul><li><a href="#" id="photoToolLink">फोटो कॉम्प्रेसर</a></li><li><a href="#" id="resizeToolLink">इमेज रिसाइज़र</a></li><li><a href="#" id="pdfToolLink">PDF से PNG</a></li><li><a href="#" id="pngToPdfFooterLink">PNG से PDF</a></li><li><a href="#" id="bgRemoveFooterLink">बैकग्राउंड हटाएँ</a></li></ul></div>
                <div class="footer-contact"><h3>संपर्क</h3><p><i class="fas fa-map-marker-alt"></i> बसंत पट्टी</p><p><i class="fas fa-phone"></i> +91 72098 90909</p><p><i class="fas fa-envelope"></i> sujitcsc@gmail.com</p></div>
            </div>
            <div class="copyright"><p>&copy; 2025 SUJIT CSC CYBER</p></div>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Tab Switching
            function showTool(tool) {
                document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
                document.querySelectorAll('.tool-container').forEach(cont => cont.classList.remove('active'));
                document.getElementById(tool + 'TabBtn').classList.add('active');
                document.getElementById(tool + 'Tool').classList.add('active');
            }
            
            document.getElementById('photoTabBtn').onclick = () => showTool('photo');
            document.getElementById('resizeTabBtn').onclick = () => showTool('resize');
            document.getElementById('pdfTabBtn').onclick = () => showTool('pdf');
            document.getElementById('pngToPdfTabBtn').onclick = () => showTool('pngToPdf');
            document.getElementById('bgRemoveTabBtn').onclick = () => showTool('bgRemove');
            document.getElementById('photoToolLink').onclick = (e) => { e.preventDefault(); showTool('photo'); };
            document.getElementById('resizeToolLink').onclick = (e) => { e.preventDefault(); showTool('resize'); };
            document.getElementById('pdfToolLink').onclick = (e) => { e.preventDefault(); showTool('pdf'); };
            document.getElementById('pngToPdfFooterLink').onclick = (e) => { e.preventDefault(); showTool('pngToPdf'); };
            document.getElementById('bgRemoveFooterLink').onclick = (e) => { e.preventDefault(); showTool('bgRemove'); };
            
            function formatFileSize(bytes) {
                if (bytes === 0) return '0 Bytes';
                const k = 1024;
                const sizes = ['Bytes', 'KB', 'MB'];
                const i = Math.floor(Math.log(bytes) / Math.log(k));
                return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
            }
            
            function showAlert(message, isError = false) {
                const alertDiv = document.createElement('div');
                alertDiv.className = 'alert-message';
                alertDiv.style.backgroundColor = isError ? '#e74c3c' : '#27ae60';
                alertDiv.innerHTML = `<i class="fas ${isError ? 'fa-exclamation-triangle' : 'fa-check-circle'}"></i> ${message}`;
                document.body.appendChild(alertDiv);
                setTimeout(() => alertDiv.remove(), 3000);
            }
            
            // ========== PHOTO COMPRESSOR ==========
            let photoFile = null, compressedBlob = null;
            const photoInput = document.getElementById('photoFileInput');
            document.getElementById('photoUploadArea').onclick = () => photoInput.click();
            photoInput.onchange = (e) => {
                if (e.target.files[0]) {
                    photoFile = e.target.files[0];
                    document.getElementById('originalSize').textContent = `आकार: ${formatFileSize(photoFile.size)}`;
                    const reader = new FileReader();
                    reader.onload = (ev) => {
                        const img = new Image();
                        img.onload = () => {
                            document.getElementById('originalDimensions').textContent = `डाइमेंशन: ${img.width}×${img.height}`;
                            document.getElementById('originalImage').innerHTML = '';
                            document.getElementById('originalImage').appendChild(img);
                        };
                        img.src = ev.target.result;
                    };
                    reader.readAsDataURL(photoFile);
                }
            };
            
            document.getElementById('compressBtn').onclick = () => {
                if (!photoFile) { showAlert('कृपया पहले फोटो अपलोड करें', true); return; }
                const quality = parseInt(document.getElementById('quality').value) / 100;
                const maxWidth = parseInt(document.getElementById('maxWidth').value);
                const img = new Image();
                img.onload = () => {
                    let w = img.width, h = img.height;
                    if (w > maxWidth) { h = (h * maxWidth) / w; w = maxWidth; }
                    const canvas = document.createElement('canvas');
                    canvas.width = w; canvas.height = h;
                    canvas.getContext('2d').drawImage(img, 0, 0, w, h);
                    canvas.toBlob(blob => {
                        compressedBlob = blob;
                        const url = URL.createObjectURL(blob);
                        const newImg = new Image();
                        newImg.onload = () => {
                            document.getElementById('compressedImage').innerHTML = '';
                            document.getElementById('compressedImage').appendChild(newImg);
                            document.getElementById('compressedSize').textContent = `आकार: ${formatFileSize(blob.size)}`;
                            document.getElementById('compressedDimensions').textContent = `डाइमेंशन: ${Math.round(w)}×${Math.round(h)}`;
                            const reduction = ((photoFile.size - blob.size) / photoFile.size * 100).toFixed(1);
                            document.getElementById('sizeReduction').textContent = `${reduction}%`;
                            document.getElementById('compressionRatio').textContent = `${(photoFile.size / blob.size).toFixed(1)}:1`;
                            document.getElementById('downloadPhotoBtn').disabled = false;
                            showAlert('फोटो कॉम्प्रेस सफलतापूर्वक हुआ!');
                        };
                        newImg.src = url;
                    }, 'image/jpeg', quality);
                };
                img.src = URL.createObjectURL(photoFile);
            };
            
            document.getElementById('downloadPhotoBtn').onclick = () => {
                if (compressedBlob) {
                    const a = document.createElement('a');
                    a.href = URL.createObjectURL(compressedBlob);
                    a.download = 'compressed_image.jpg';
                    a.click();
                }
            };
            
            document.getElementById('resetPhotoBtn').onclick = () => {
                photoInput.value = '';
                photoFile = null;
                compressedBlob = null;
                document.getElementById('originalImage').innerHTML = '<i class="fas fa-image" style="font-size: 3rem;"></i><p>मूल फोटो</p>';
                document.getElementById('compressedImage').innerHTML = '<i class="fas fa-file-archive" style="font-size: 3rem;"></i><p>कम्प्रेस्ड फोटो</p>';
                document.getElementById('downloadPhotoBtn').disabled = true;
                document.getElementById('originalSize').textContent = 'आकार: --';
                document.getElementById('originalDimensions').textContent = 'डाइमेंशन: --';
                document.getElementById('compressedSize').textContent = 'आकार: --';
                document.getElementById('compressedDimensions').textContent = 'डाइमेंशन: --';
                document.getElementById('sizeReduction').textContent = '--';
                document.getElementById('compressionRatio').textContent = '--';
            };
            
            document.getElementById('quality').oninput = () => document.getElementById('qualityValue').textContent = document.getElementById('quality').value;
            document.getElementById('maxWidth').oninput = () => document.getElementById('widthValue').textContent = document.getElementById('maxWidth').value;
            
            // ========== IMAGE RESIZER - FIXED ==========
            let resizeFile = null, resizedBlob = null;
            let originalResizeW = 0, originalResizeH = 0;
            
            const resizeInput = document.getElementById('resizeFileInput');
            const resizeArea = document.getElementById('resizeUploadArea');
            const resizeWidth = document.getElementById('resizeWidth');
            const resizeHeight = document.getElementById('resizeHeight');
            const maintainRatio = document.getElementById('maintainAspectRatio');
            const outputFormat = document.getElementById('outputFormatResize');
            const kbSlider = document.getElementById('kbTargetSlider');
            const targetSizeDisplay = document.getElementById('targetSizeDisplay');
            
            resizeArea.onclick = () => resizeInput.click();
            resizeInput.onchange = (e) => {
                if (e.target.files[0]) {
                    resizeFile = e.target.files[0];
                    document.getElementById('originalResizeSize').textContent = `आकार: ${formatFileSize(resizeFile.size)}`;
                    const reader = new FileReader();
                    reader.onload = (ev) => {
                        const img = new Image();
                        img.onload = () => {
                            originalResizeW = img.width;
                            originalResizeH = img.height;
                            document.getElementById('originalResizeDimensions').textContent = `डाइमेंशन: ${originalResizeW}×${originalResizeH}`;
                            document.getElementById('aspectRatioDisplay').textContent = `मूल अनुपात: ${(originalResizeW/originalResizeH).toFixed(2)}:1`;
                            document.getElementById('originalResizeImage').innerHTML = '';
                            document.getElementById('originalResizeImage').appendChild(img);
                            resizeWidth.value = originalResizeW;
                            resizeHeight.value = originalResizeH;
                        };
                        img.src = ev.target.result;
                    };
                    reader.readAsDataURL(resizeFile);
                }
            };
            
            function updateDimensions() {
                if (maintainRatio.checked && originalResizeW && originalResizeH) {
                    const newWidth = parseInt(resizeWidth.value);
                    if (!isNaN(newWidth) && newWidth > 0) {
                        const newHeight = Math.round(originalResizeH * (newWidth / originalResizeW));
                        resizeHeight.value = newHeight;
                    }
                }
            }
            
            function updateDimensionsFromHeight() {
                if (maintainRatio.checked && originalResizeW && originalResizeH) {
                    const newHeight = parseInt(resizeHeight.value);
                    if (!isNaN(newHeight) && newHeight > 0) {
                        const newWidth = Math.round(originalResizeW * (newHeight / originalResizeH));
                        resizeWidth.value = newWidth;
                    }
                }
            }
            
            resizeWidth.addEventListener('input', updateDimensions);
            resizeHeight.addEventListener('input', updateDimensionsFromHeight);
            
            // Resize by Dimensions
            document.getElementById('resizeBtn').onclick = () => {
                if (!resizeFile) { showAlert('कृपया पहले इमेज अपलोड करें', true); return; }
                const targetW = parseInt(resizeWidth.value);
                const targetH = parseInt(resizeHeight.value);
                const format = outputFormat.value;
                
                const img = new Image();
                img.onload = () => {
                    const canvas = document.createElement('canvas');
                    canvas.width = targetW;
                    canvas.height = targetH;
                    canvas.getContext('2d').drawImage(img, 0, 0, targetW, targetH);
                    canvas.toBlob(blob => {
                        resizedBlob = blob;
                        const url = URL.createObjectURL(blob);
                        const newImg = new Image();
                        newImg.onload = () => {
                            document.getElementById('resizedImage').innerHTML = '';
                            document.getElementById('resizedImage').appendChild(newImg);
                            document.getElementById('resizedSize').textContent = `आकार: ${formatFileSize(blob.size)}`;
                            document.getElementById('resizedDimensions').textContent = `डाइमेंशन: ${targetW}×${targetH}`;
                            const change = ((blob.size - resizeFile.size) / resizeFile.size * 100).toFixed(1);
                            document.getElementById('resizeChange').textContent = `${change > 0 ? '+' : ''}${change}%`;
                            document.getElementById('targetAchieved').textContent = 'डाइमेंशन रिसाइज़';
                            document.getElementById('downloadResizeBtn').disabled = false;
                            showAlert('इमेज सफलतापूर्वक रिसाइज़ हुई!');
                        };
                        newImg.src = url;
                    }, format, 0.92);
                };
                img.src = URL.createObjectURL(resizeFile);
            };
            
            // Resize by KB Target
            async function resizeByKB(targetKB) {
                if (!resizeFile) { showAlert('कृपया पहले इमेज अपलोड करें', true); return; }
                const btn = document.getElementById('resizeByKbBtn');
                btn.classList.add('loading');
                const targetBytes = targetKB * 1024;
                const format = outputFormat.value;
                let bestBlob = null;
                let low = 0.05, high = 0.95;
                
                const width = parseInt(resizeWidth.value);
                const height = parseInt(resizeHeight.value);
                
                for (let i = 0; i < 10; i++) {
                    const testQuality = (low + high) / 2;
                    const img = new Image();
                    const result = await new Promise((resolve) => {
                        img.onload = () => {
                            const canvas = document.createElement('canvas');
                            canvas.width = width;
                            canvas.height = height;
                            canvas.getContext('2d').drawImage(img, 0, 0, width, height);
                            canvas.toBlob(blob => resolve({ blob, quality: testQuality }), format, testQuality);
                        };
                        img.src = URL.createObjectURL(resizeFile);
                    });
                    
                    if (result.blob.size <= targetBytes) {
                        bestBlob = result.blob;
                        low = testQuality;
                    } else {
                        high = testQuality;
                    }
                }
                
                if (!bestBlob) {
                    const img = new Image();
                    await new Promise((resolve) => {
                        img.onload = () => {
                            const canvas = document.createElement('canvas');
                            canvas.width = width;
                            canvas.height = height;
                            canvas.getContext('2d').drawImage(img, 0, 0, width, height);
                            canvas.toBlob(blob => { bestBlob = blob; resolve(); }, format, 0.05);
                        };
                        img.src = URL.createObjectURL(resizeFile);
                    });
                }
                
                resizedBlob = bestBlob;
                const url = URL.createObjectURL(bestBlob);
                const newImg = new Image();
                newImg.onload = () => {
                    document.getElementById('resizedImage').innerHTML = '';
                    document.getElementById('resizedImage').appendChild(newImg);
                    document.getElementById('resizedSize').textContent = `आकार: ${formatFileSize(bestBlob.size)}`;
                    document.getElementById('resizedDimensions').textContent = `डाइमेंशन: ${newImg.width}×${newImg.height}`;
                    const change = ((bestBlob.size - resizeFile.size) / resizeFile.size * 100).toFixed(1);
                    document.getElementById('resizeChange').textContent = `${change > 0 ? '+' : ''}${change}%`;
                    const diff = ((bestBlob.size - targetBytes) / targetBytes * 100).toFixed(1);
                    document.getElementById('targetAchieved').innerHTML = `${Math.abs(diff)}% ${diff <= 0 ? 'लक्ष्य से कम' : 'लक्ष्य से अधिक'}`;
                    document.getElementById('downloadResizeBtn').disabled = false;
                    btn.classList.remove('loading');
                    showAlert(`${targetKB}KB लक्ष्य के अनुसार रिसाइज़ पूर्ण!`);
                };
                newImg.src = url;
            }
            
            document.getElementById('resizeByKbBtn').onclick = () => {
                const targetKB = parseInt(kbSlider.value);
                resizeByKB(targetKB);
            };
            
            kbSlider.oninput = () => {
                targetSizeDisplay.textContent = `लक्ष्य आकार: ${kbSlider.value} KB`;
            };
            
            // KB Preset Buttons
            document.querySelectorAll('#resizeTool .preset-btn[data-kb]').forEach(btn => {
                btn.onclick = () => {
                    const kb = parseInt(btn.dataset.kb);
                    kbSlider.value = kb;
                    targetSizeDisplay.textContent = `लक्ष्य आकार: ${kb} KB`;
                    if (resizeFile) resizeByKB(kb);
                };
            });
            
            document.getElementById('downloadResizeBtn').onclick = () => {
                if (resizedBlob) {
                    const ext = outputFormat.value.split('/')[1];
                    const a = document.createElement('a');
                    a.href = URL.createObjectURL(resizedBlob);
                    a.download = `resized_image.${ext === 'jpeg' ? 'jpg' : ext}`;
                    a.click();
                }
            };
            
            document.getElementById('resetResizeBtn').onclick = () => {
                resizeInput.value = '';
                resizeFile = null;
                resizedBlob = null;
                originalResizeW = 0; originalResizeH = 0;
                document.getElementById('originalResizeImage').innerHTML = '<i class="fas fa-image" style="font-size: 3rem;"></i><p>मूल इमेज</p>';
                document.getElementById('resizedImage').innerHTML = '<i class="fas fa-expand-alt" style="font-size: 3rem;"></i><p>रिसाइज़ की गई इमेज</p>';
                document.getElementById('downloadResizeBtn').disabled = true;
                resizeWidth.value = 800;
                resizeHeight.value = 600;
                document.getElementById('originalResizeSize').textContent = 'आकार: --';
                document.getElementById('originalResizeDimensions').textContent = 'डाइमेंशन: --';
                document.getElementById('resizedSize').textContent = 'आकार: --';
                document.getElementById('resizedDimensions').textContent = 'डाइमेंशन: --';
                document.getElementById('resizeChange').textContent = '--';
                document.getElementById('targetAchieved').textContent = '--';
            };
            
            // ========== PDF TO PNG - FIXED ==========
            let pdfResultBlob = null;
            let pdfPages = [];
            document.getElementById('pdfUploadArea').onclick = () => document.getElementById('pdfFileInput').click();
            
            document.getElementById('pdfFileInput').onchange = async (e) => {
                if (e.target.files[0]) {
                    const file = e.target.files[0];
                    showAlert('PDF लोड हो रहा है...');
                    const arrayBuffer = await file.arrayBuffer();
                    const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
                    const numPages = pdf.numPages;
                    document.getElementById('pdfInfo').style.display = 'block';
                    document.getElementById('pdfPageCount').textContent = `पृष्ठ: ${numPages}`;
                    pdfPages = [];
                    const firstPage = await pdf.getPage(1);
                    const viewport = firstPage.getViewport({ scale: 1.5 });
                    const canvas = document.createElement('canvas');
                    const context = canvas.getContext('2d');
                    canvas.width = viewport.width;
                    canvas.height = viewport.height;
                    await firstPage.render({ canvasContext: context, viewport: viewport }).promise;
                    document.getElementById('pdfPreview').innerHTML = '';
                    const img = document.createElement('img');
                    img.src = canvas.toDataURL();
                    img.style.maxWidth = '100%';
                    img.style.maxHeight = '200px';
                    document.getElementById('pdfPreview').appendChild(img);
                    document.getElementById('pdfPreview').appendChild(document.createElement('p')).textContent = `PDF प्रीव्यू (पहला पृष्ठ)`;
                    showAlert('PDF सफलतापूर्वक लोड हुआ! अब कन्वर्ट करें।');
                }
            };
            
            document.getElementById('convertPdfBtn').onclick = async () => {
                if (!document.getElementById('pdfFileInput').files[0]) {
                    showAlert('कृपया पहले PDF फाइल अपलोड करें', true);
                    return;
                }
                showAlert('PDF को PNG में बदला जा रहा है...');
                const file = document.getElementById('pdfFileInput').files[0];
                const arrayBuffer = await file.arrayBuffer();
                const pdf = await pdfjsLib.getDocument({ data: arrayBuffer }).promise;
                const numPages = pdf.numPages;
                const pages = [];
                
                for (let i = 1; i <= numPages; i++) {
                    const page = await pdf.getPage(i);
                    const viewport = page.getViewport({ scale: 2 });
                    const canvas = document.createElement('canvas');
                    const context = canvas.getContext('2d');
                    canvas.width = viewport.width;
                    canvas.height = viewport.height;
                    await page.render({ canvasContext: context, viewport: viewport }).promise;
                    pages.push(canvas.toDataURL('image/png'));
                }
                
                if (pages.length > 0) {
                    // Create a ZIP of all PNGs or just first page preview
                    if (pages.length === 1) {
                        const pngBlob = await fetch(pages[0]).then(r => r.blob());
                        pdfResultBlob = pngBlob;
                        document.getElementById('downloadPdfResultBtn').disabled = false;
                        showAlert('PDF को PNG में बदल दिया गया!');
                    } else {
                        // Create ZIP for multiple pages
                        const zip = new JSZip();
                        for (let i = 0; i < pages.length; i++) {
                            const pngBlob = await fetch(pages[i]).then(r => r.blob());
                            zip.file(`page_${i+1}.png`, pngBlob);
                        }
                        pdfResultBlob = await zip.generateAsync({ type: 'blob' });
                        document.getElementById('downloadPdfResultBtn').disabled = false;
                        showAlert(`${numPages} पृष्ठों को PNG में बदल दिया गया! ZIP फाइल डाउनलोड होगी।`);
                    }
                }
            };
            
            document.getElementById('downloadPdfResultBtn').onclick = () => {
                if (pdfResultBlob) {
                    const a = document.createElement('a');
                    a.href = URL.createObjectURL(pdfResultBlob);
                    const fileName = pdfResultBlob.type === 'application/zip' ? 'pdf_pages.zip' : 'converted_page.png';
                    a.download = fileName;
                    a.click();
                }
            };
            
            document.getElementById('resetPdfBtn').onclick = () => {
                document.getElementById('pdfFileInput').value = '';
                pdfPages = [];
                pdfResultBlob = null;
                document.getElementById('pdfPreview').innerHTML = '<i class="fas fa-file-pdf" style="font-size: 3rem;"></i><p>PDF प्रीव्यू</p>';
                document.getElementById('pdfInfo').style.display = 'none';
                document.getElementById('downloadPdfResultBtn').disabled = true;
            };
            
            // ========== PNG TO PDF ==========
            let pngImagesList = [], pdfFinalBlob = null;
            document.getElementById('pngUploadArea').onclick = () => document.getElementById('pngFileInput').click();
            document.getElementById('pngFileInput').onchange = (e) => {
                pngImagesList = [];
                Array.from(e.target.files).forEach(file => {
                    if (file.type.startsWith('image/')) {
                        const reader = new FileReader();
                        reader.onload = (ev) => pngImagesList.push(ev.target.result);
                        reader.readAsDataURL(file);
                    }
                });
                setTimeout(() => {
                    document.getElementById('imageCount').textContent = `इमेज: ${pngImagesList.length}`;
                    if (pngImagesList.length) {
                        document.getElementById('pngPreviewArea').innerHTML = `<img src="${pngImagesList[0]}" style="max-height:150px;"><p>${pngImagesList.length} इमेज</p>`;
                    } else {
                        document.getElementById('pngPreviewArea').innerHTML = '<i class="fas fa-images"></i><p>इमेज प्रीव्यू</p>';
                    }
                }, 500);
            };
            
            document.getElementById('convertToPdfBtn').onclick = async () => {
                if (!pngImagesList.length) { showAlert('पहले इमेज अपलोड करें', true); return; }
                const { jsPDF } = window.jspdf;
                let pdf = null;
                for (let i = 0; i < pngImagesList.length; i++) {
                    const img = new Image();
                    await new Promise(resolve => { img.onload = resolve; img.src = pngImagesList[i]; });
                    let w = img.width, h = img.height;
                    let pdfW = w * 0.264583, pdfH = h * 0.264583;
                    if (!pdf) pdf = new jsPDF({ unit: 'mm', format: [pdfW, pdfH] });
                    else pdf.addPage([pdfW, pdfH]);
                    pdf.addImage(pngImagesList[i], 'PNG', 0, 0, pdfW, pdfH);
                }
                if (pdf) {
                    pdfFinalBlob = pdf.output('blob');
                    document.getElementById('downloadPdfBtn2').disabled = false;
                    showAlert('PDF तैयार है! डाउनलोड करें');
                }
            };
            
            document.getElementById('downloadPdfBtn2').onclick = () => {
                if (pdfFinalBlob) {
                    const a = document.createElement('a');
                    a.href = URL.createObjectURL(pdfFinalBlob);
                    a.download = 'converted.pdf';
                    a.click();
                }
            };
            
            document.getElementById('resetPngToPdfBtn').onclick = () => {
                document.getElementById('pngFileInput').value = '';
                pngImagesList = [];
                pdfFinalBlob = null;
                document.getElementById('pngPreviewArea').innerHTML = '<i class="fas fa-images"></i><p>इमेज प्रीव्यू</p>';
                document.getElementById('imageCount').textContent = 'इमेज: 0';
                document.getElementById('downloadPdfBtn2').disabled = true;
            };
            
            // ========== REMOVE BACKGROUND TOOL - FIXED ==========
            let bgOriginalFile = null, bgResultBlob = null;
            const bgUploadArea = document.getElementById('bgUploadArea');
            const bgFileInput = document.getElementById('bgFileInput');
            const removeBgBtn = document.getElementById('removeBgBtn');
            const resetBgBtn = document.getElementById('resetBgBtn');
            const downloadBgBtn = document.getElementById('downloadBgBtn');
            const bgOutputType = document.getElementById('bgOutputType');
            const customBgColor = document.getElementById('customBgColor');
            const edgeSmoothing = document.getElementById('edgeSmoothing');
            
            bgUploadArea.onclick = () => bgFileInput.click();
            bgFileInput.onchange = (e) => {
                if(e.target.files[0]) {
                    bgOriginalFile = e.target.files[0];
                    document.getElementById('originalBgSize').textContent = `आकार: ${formatFileSize(bgOriginalFile.size)}`;
                    const reader = new FileReader();
                    reader.onload = (ev) => {
                        const img = new Image();
                        img.onload = () => {
                            document.getElementById('originalBgDimensions').textContent = `डाइमेंशन: ${img.width}×${img.height}`;
                            document.getElementById('originalBgImage').innerHTML = '';
                            document.getElementById('originalBgImage').appendChild(img);
                        };
                        img.src = ev.target.result;
                    };
                    reader.readAsDataURL(bgOriginalFile);
                }
            };
            
            async function removeBackground() {
                if(!bgOriginalFile) { showAlert('पहले फोटो अपलोड करें', true); return; }
                removeBgBtn.classList.add('loading');
                const img = new Image();
                const imgUrl = URL.createObjectURL(bgOriginalFile);
                img.src = imgUrl;
                await new Promise(r => { img.onload = r; });
                const canvas = document.createElement('canvas');
                canvas.width = img.width;
                canvas.height = img.height;
                const ctx = canvas.getContext('2d');
                ctx.drawImage(img, 0, 0);
                const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
                const data = imageData.data;
                
                // Simple foreground extraction based on center region
                const centerX = canvas.width/2, centerY = canvas.height/2;
                const centerIdx = (Math.floor(centerY)*canvas.width + Math.floor(centerX))*4;
                const refR = data[centerIdx], refG = data[centerIdx+1], refB = data[centerIdx+2];
                const threshold = 70;
                
                for(let i=0; i<data.length; i+=4) {
                    const r = data[i], g=data[i+1], b=data[i+2];
                    const diff = Math.abs(r-refR)+Math.abs(g-refG)+Math.abs(b-refB);
                    let alpha = diff < threshold ? 255 : (diff > threshold+50 ? 0 : Math.max(0, Math.min(255, 255 - ((diff-threshold)*5))));
                    data[i+3] = alpha;
                }
                ctx.putImageData(imageData,0,0);
                
                const outputCanvas = document.createElement('canvas');
                outputCanvas.width = canvas.width;
                outputCanvas.height = canvas.height;
                const outCtx = outputCanvas.getContext('2d');
                const bgType = bgOutputType.value;
                if(bgType === 'white') {
                    outCtx.fillStyle = '#ffffff';
                    outCtx.fillRect(0,0,outputCanvas.width,outputCanvas.height);
                    outCtx.drawImage(canvas,0,0);
                } else if(bgType === 'custom') {
                    outCtx.fillStyle = customBgColor.value;
                    outCtx.fillRect(0,0,outputCanvas.width,outputCanvas.height);
                    outCtx.drawImage(canvas,0,0);
                } else {
                    outCtx.clearRect(0,0,outputCanvas.width,outputCanvas.height);
                    outCtx.drawImage(canvas,0,0);
                }
                const resultBlob = await new Promise(resolve => outputCanvas.toBlob(resolve, 'image/png'));
                bgResultBlob = resultBlob;
                const previewUrl = URL.createObjectURL(resultBlob);
                const resultImg = new Image();
                resultImg.onload = () => {
                    document.getElementById('removedBgImage').innerHTML = '';
                    document.getElementById('removedBgImage').appendChild(resultImg);
                    document.getElementById('removedBgSize').textContent = `आकार: ${formatFileSize(resultBlob.size)}`;
                    document.getElementById('removedBgDimensions').textContent = `डाइमेंशन: ${outputCanvas.width}×${outputCanvas.height}`;
                    downloadBgBtn.disabled = false;
                    removeBgBtn.classList.remove('loading');
                    showAlert('बैकग्राउंड सफलतापूर्वक हटा दिया गया!');
                };
                resultImg.src = previewUrl;
                URL.revokeObjectURL(imgUrl);
            }
            removeBgBtn.onclick = removeBackground;
            resetBgBtn.onclick = () => {
                bgFileInput.value = '';
                bgOriginalFile = null;
                bgResultBlob = null;
                document.getElementById('originalBgImage').innerHTML = '<i class="fas fa-image" style="font-size: 3rem;"></i><p>मूल इमेज</p>';
                document.getElementById('removedBgImage').innerHTML = '<i class="fas fa-sticky-note" style="font-size: 3rem;"></i><p>हटाया गया बैकग्राउंड</p>';
                document.getElementById('downloadBgBtn').disabled = true;
                document.getElementById('originalBgSize').textContent = 'आकार: --';
                document.getElementById('originalBgDimensions').textContent = 'डाइमेंशन: --';
                document.getElementById('removedBgSize').textContent = 'आकार: --';
                document.getElementById('removedBgDimensions').textContent = 'डाइमेंशन: --';
            };
            downloadBgBtn.onclick = () => {
                if(bgResultBlob) {
                    const a = document.createElement('a');
                    a.href = URL.createObjectURL(bgResultBlob);
                    a.download = 'removed_bg.png';
                    a.click();
                }
            };
        });
    </script>
</body>
</html>
