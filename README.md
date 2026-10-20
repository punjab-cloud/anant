# anant<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quotation - Janak Positioning & Surveying Systems</title>
    <style>
        body { 
            font-family: 'Times New Roman', Times, serif; 
            color: #000; 
            line-height: 1.4; 
            margin: 0; 
            padding: 20px; 
            background-color: #f4f4f9; 
        }
        
        :root {
            --primary-saffron: #D65E00; 
            --light-saffron: #FFF3EB;
        }

        /* --- LOGIN SCREEN STYLES --- */
        #login-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background-color: #f4f4f9; z-index: 9999;
            display: flex; justify-content: center; align-items: center;
        }
        .login-box {
            background: #fff; padding: 40px; border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1); text-align: center;
            border-top: 5px solid var(--primary-saffron); width: 300px;
        }
        .login-box h2 { margin-top: 0; color: var(--primary-saffron); letter-spacing: 1px; }
        .login-input {
            width: 100%; padding: 10px; margin: 10px 0;
            border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box;
            font-family: 'Times New Roman', Times, serif; font-size: 16px;
        }
        .login-btn {
            background-color: var(--primary-saffron); color: white; border: none;
            padding: 10px 20px; font-weight: bold; cursor: pointer; width: 100%;
            border-radius: 4px; margin-top: 10px; font-size: 16px;
        }
        .login-btn:hover { background-color: #b34e00; }
        .error-msg { color: #dc3545; font-size: 14px; display: none; margin-top: 10px; font-weight: bold; }

        /* HIDE MAIN CONTENT INITIALLY */
        #main-content { display: none; }

        /* --- QUOTATION STYLES --- */
        .invoice-box { position: relative; max-width: 1000px; margin: auto; padding: 35px; border: 1px solid #ccc; box-shadow: 0 0 15px rgba(0, 0, 0, 0.1); background: #fff; overflow: hidden; }
        
        .watermark {
            position: absolute;
            top: 50%; left: 50%;
            transform: translate(-50%, -50%) rotate(-45deg);
            font-size: 160px; color: rgba(214, 94, 0, 0.06); font-weight: bold;
            z-index: 0; pointer-events: none; user-select: none; white-space: nowrap;
        }
        
        .content-layer { position: relative; z-index: 1; }
        .header-flex { display: flex; justify-content: space-between; align-items: flex-start; border-bottom: 3px solid var(--primary-saffron); padding-bottom: 20px; margin-bottom: 20px; }
        .logo-container { flex: 1; }
        .logo-text { font-size: 26px; font-weight: bold; color: var(--primary-saffron); letter-spacing: 1px; margin: 0 0 5px 0; line-height: 1.2; text-transform: uppercase; }
        .company-address { font-size: 13px; color: #333; line-height: 1.5; }
        .company-address strong { color: #000; }
        .quote-title { text-align: right; min-width: 200px; }
        .quote-title h1 { margin: 0 0 5px 0; color: var(--primary-saffron); font-size: 26px; text-transform: uppercase; letter-spacing: 2px; }
        .date-field { font-size: 14px; font-weight: bold; }
        .editable-input { border: 1px dashed #bbb; background: #fafafa; padding: 3px 6px; font-family: inherit; font-size: inherit; transition: background 0.3s; }
        .editable-input:focus { background: var(--light-saffron); outline: 1px solid var(--primary-saffron); border-style: solid; }
        .editable-num { width: 110px; text-align: right; font-weight: bold; }
        .editable-desc { 
            width: 100%; min-height: 150px; box-sizing: border-box; font-size: 12.5px; 
            line-height: 1.6; white-space: pre-wrap; padding: 8px; background: #fff;
            border: 1px dashed #ccc; margin-top: 5px;
        }
        .model-select { width: 100%; padding: 8px; border: 1px solid var(--primary-saffron); background: #fff; font-family: 'Times New Roman', Times, serif; font-weight: bold; font-size: 14px; color: #000; cursor: pointer; }
        .model-select optgroup { background: #eee; font-style: italic; }
        .model-select option { background: #fff; font-style: normal; }
        .address-block { margin-bottom: 20px; font-size: 14px; }
        .address-block p { margin: 3px 0; }
        .client-input { width: 350px; margin-bottom: 3px; font-weight: bold; }
        table { width: 100%; border-collapse: collapse; margin-bottom: 20px; font-size: 14px; border: 1px solid #000; background: transparent; }
        table, th, td { border: 1px solid #000; } 
        th, td { padding: 12px; text-align: left; vertical-align: top; }
        th { background-color: var(--primary-saffron); color: white; font-size: 15px; letter-spacing: 0.5px; }
        .text-right { text-align: right; }
        .text-center { text-align: center; }
        .row-num { font-weight: bold; text-align: center; font-size: 16px; }
        .totals-row td { font-weight: bold; background-color: rgba(244, 244, 249, 0.8); font-size: 15px; }
        .grand-total { font-size: 18px !important; color: var(--primary-saffron); }
        .action-btns { margin-bottom: 25px; }
        .add-row-btn { background-color: var(--primary-saffron); color: white; border: none; padding: 10px 20px; font-family: 'Times New Roman', Times, serif; font-size: 15px; font-weight: bold; cursor: pointer; border-radius: 2px; }
        .add-row-btn:hover { background-color: #b34e00; }
        .delete-btn { background-color: #dc3545; color: white; border: none; padding: 6px 12px; font-family: 'Times New Roman', Times, serif; font-size: 12px; font-weight: bold; cursor: pointer; margin-top: 5px; }
        .terms-section { font-size: 13px; margin-bottom: 20px; }
        .terms-section h4 { margin-bottom: 10px; color: var(--primary-saffron); border-bottom: 1px solid #ccc; padding-bottom: 5px; font-size: 15px; }
        .terms-grid { display: grid; grid-template-columns: 100px 1fr; row-gap: 6px; }
        .signoff { margin-top: 30px; font-size: 14px; }
        .signature-box { margin-top: 40px; display: flex; justify-content: space-between; }
        .print-btn-container { text-align: center; margin-top: 30px; margin-bottom: 30px; }
        .print-btn { background-color: #28a745; color: white; border: none; padding: 12px 30px; font-family: 'Times New Roman', Times, serif; font-size: 18px; font-weight: bold; cursor: pointer; border-radius: 3px; }

        @media print {
            body { background-color: #fff; padding: 0; margin: 0; }
            #login-overlay { display: none !important; }
            #main-content { display: block !important; }
            .invoice-box { box-shadow: none; border: none; padding: 0; max-width: 100%; }
            .print-btn-container, .action-btns, .delete-btn, .model-select { display: none !important; }
            .editable-input, .editable-desc { border: none; background: transparent; padding: 0; }
            .editable-desc { min-height: auto; margin-top: 0; }
            table, th, td { border: 1px solid #000 !important; }
            th { background-color: var(--primary-saffron) !important; color: white !important; -webkit-print-color-adjust: exact; print-color-adjust: exact; }
            .totals-row td { background-color: #f4f4f9 !important; -webkit-print-color-adjust: exact; print-color-adjust: exact; }
            .watermark { color: rgba(214, 94, 0, 0.08) !important; -webkit-print-color-adjust: exact; print-color-adjust: exact; }
        }
    </style>
</head>
<body>

<!-- LOGIN OVERLAY -->
<div id="login-overlay">
    <div class="login-box">
        <h2>SECURE ACCESS</h2>
        <input type="text" id="username" class="login-input" placeholder="Username" onkeypress="handleEnter(event)">
        <input type="password" id="password" class="login-input" placeholder="Password" onkeypress="handleEnter(event)">
        <button class="login-btn" onclick="checkLogin()">Login to Generator</button>
        <div id="errorMsg" class="error-msg">Invalid credentials. Access denied.</div>
    </div>
</div>

<!-- MAIN APPLICATION -->
<div id="main-content">
    <div class="invoice-box">
        <!-- Background Watermark -->
        <div class="watermark">JANAK</div>

        <!-- Content Layer -->
        <div class="content-layer">
            <!-- Header -->
            <div class="header-flex">
                <div class="logo-container">
                    <div class="logo-text"><strong>Janak Positioning & Surveying Systems Pvt Ltd.</strong>[cite: 6]</div>
                    <div class="company-address">
                        B-28, Sector -4, Noida, Uttar Pradesh -201301<br>[cite: 6]
                        H.O: 304B, Pal Mohan Plaza 11/56 D.B Gupta Road, Karol Bagh, New Delhi-110005<br>[cite: 6]
                        <strong>GSTIN/UIN:</strong> 09AABCJ0148A1Z5 &nbsp;|&nbsp; <strong>Ph:</strong> 9811008317[cite: 6]
                    </div>
                </div>
                <div class="quote-title">
                    <h1>QUOTATION</h1>
                    <div class="date-field">
                        Date: <input type="text" class="editable-input" value="18-10-2026" id="quoteDate" style="width: 90px;">
                    </div>
                </div>
            </div>

            <!-- Client Address Block -->
            <div class="address-block">
                <p><strong>To,</strong></p>
                <p><input type="text" class="editable-input client-input" value="Client Company Name" id="clientName" placeholder="Client Company Name"></p>
                <p><input type="text" class="editable-input client-input" value="Street Address / Area" id="clientAddress1" placeholder="Street Address / Area"></p>
                <p><input type="text" class="editable-input client-input" value="City, State, Pincode" id="clientAddress2" placeholder="City, State, Pincode"></p>
            </div>

            <!-- Editable Greeting -->
            <p style="margin-bottom: 5px;">
                <input type="text" class="editable-input" value="Dear Sir/Madam," style="font-size: 14px; font-weight: bold; width: 250px;">
            </p>
            
            <!-- Editable Professional Intro Line -->
            <div class="editable-input" contenteditable="true" style="font-size: 14px; margin-top: 0; margin-bottom: 20px; padding: 4px; min-height: 20px;">
                Thank you for your recent inquiry regarding our high-precision GNSS Surveying Instruments and Antennas. We are pleased to submit the following competitive commercial proposal for your review:
            </div>

            <!-- Products Table -->
            <table id="mainTable">
                <thead>
                    <tr>
                        <th style="width: 5%;" class="text-center">S.No.</th>
                        <th style="width: 65%;">Technical Descriptions</th>
                        <th style="width: 15%;" class="text-right">Unit Price</th>
                        <th style="width: 15%;" class="text-right">Total Price</th>
                        <th style="width: 3%;" class="text-center no-print"></th>
                    </tr>
                </thead>
                <tbody id="itemsTableBody">
                    <!-- Rows dynamically added via JavaScript -->
                </tbody>
            </table>

            <!-- ADD BUTTON -->
            <div class="action-btns no-print">
                <button class="add-row-btn" onclick="addNewRow()">+ Add Product</button>
            </div>

            <!-- Totals Section -->
            <table>
                <tr class="totals-row">
                    <td colspan="3" class="text-right" style="width: 85%;">Total</td>
                    <td class="text-right" id="subtotal" style="width: 15%;">Rs. 0.00</td>
                </tr>
                <tr class="totals-row">
                    <td colspan="3" class="text-right">GST 18%</td>
                    <td class="text-right" id="gstAmount">Rs. 0.00</td>
                </tr>
                <tr class="totals-row grand-total">
                    <td colspan="3" class="text-right">Grand Total</td>
                    <td class="text-right" id="grandTotal">Rs. 0.00</td>
                </tr>
            </table>

            <!-- Terms & Conditions -->
            <div class="terms-section">
                <h4>Terms &amp; Conditions:</h4>
                <div class="terms-grid">
                    <div><strong>Validity</strong></div>
                    <div>: Offer valid for 30 days</div>
                    <div><strong>Warranty</strong></div>
                    <div>: For a period of 1 year against any manufacturing defect</div>
                    <div><strong>Payment</strong></div>
                    <div>: 100% advance</div>
                    <div><strong>Tax</strong></div>
                    <div>: GST Extra 18% on above prices, additional local taxes (if applicable) extra</div>
                    <div><strong>Freight</strong></div>
                    <div>: Extra as per actual</div>
                    <div><strong>Delivery</strong></div>
                    <div>: Within 4 Weeks after order confirmation anywhere in India.</div>
                    <div><strong>Training</strong></div>
                    <div>: 2-3 days free training at your site.</div>
                </div>
                <p style="margin-top: 15px; font-size: 14px;">Purchase order to be issued in the name of <strong>"<input type="text" class="editable-input" value="M/s Janak Positioning & Surveying Systems" style="width: 290px;" id="companyName">"</strong></p>
            </div>

            <!-- Sign off -->
            <div class="signoff">
                <p>Please give us a chance to provide you with our best offers and services. For any further clarifications, please feel free to contact the undersigned.</p>
                <br>
                <p style="margin-bottom: 2px;">Best Regards,</p>
                <input type="text" class="editable-input" value="Anant Prakash" style="font-weight: bold; font-size: 14px; width: 200px; display: block; margin-bottom: 2px;">
                <input type="text" class="editable-input" value="9811008317" style="font-size: 14px; width: 200px; display: block;">
                
                <div class="signature-box">
                    <div></div>
                    <div style="text-align: right;">
                        <p>For <strong>Janak Positioning & Surveying Systems Pvt Ltd.</strong></p>[cite: 6]
                    </div>
                </div>
            </div>
        </div> <!-- End Content Layer -->
    </div>

    <div class="print-btn-container no-print">
        <button class="print-btn" onclick="window.print()">Print / Save as PDF</button>
    </div>
</div>

<!-- Scripts -->
<script>
    // --- LOGIN LOGIC ---
    function checkLogin() {
        const user = document.getElementById('username').value;
        const pass = document.getElementById('password').value;
        
        if (user === 'admin' && pass === 'Quote@janak') {
            document.getElementById('login-overlay').style.display = 'none';
            document.getElementById('main-content').style.display = 'block';
        } else {
            document.getElementById('errorMsg').style.display = 'block';
        }
    }

    function handleEnter(e) {
        if (e.key === 'Enter') {
            checkLogin();
        }
    }

    // --- QUOTATION BUILDER LOGIC ---
    const productDatabase = {
        // --- FOIF PRODUCTS ---
        "foif_a90": {
            desc: "• FOIF A90 GNSS Receiver\n• GNSS Engine: 555-channel NovAtel OEM 729 tracking engine; expandable up to or 1408 channels\n• Signal Compatibility: All-constellation tracking across GPS, GLONASS, Galileo, BeiDou, QZSS, SBAS, and NavIC/IRNSS L5\n• Accuracy:\n  - RTK: 8 mm + 0.5 ppm H / 15 mm + 0.5 ppm V\n  - Static: 3 mm + 0.1 ppm H / 3.5 mm + 0.4 ppm V (Long Static)\n  - Initialization: <10 s fix time with >99.9% reliability\n• Radio & Range: Internal 1W UHF transceiver (410–470 MHz) covering up to 5 km-8 km\n• Design & Durability: Compact magnesium-alloy build (156 mm × 76 mm), IP68 ingress protection, and rated for a 2 m drop\n• Connectivity & Power: 4G LTE, Wi-Fi WebUI, Bluetooth, Lemo/TNC I/O, and a 7.2V 6800 mAh swappable battery"
        },
        "foif_a66max": {
            desc: "• FOIF A66 Max Laser GNSS Receiver\n• GNSS Engine & Tracking: Features a 1408-channel engine that simultaneously tracks GPS, GLONASS, BDS, GALILEO, QZSS, NAVIC (IRNSS), and SBAS. Delivers RTK accuracy of ±8.0 mm + 1 ppm (horizontal) and ±15.0 mm + 1 ppm (vertical)\n• Laser Positioning Module: Integrates a laser capable of measuring distances from 0.1 to 50 meters with 1 mm resolution, achieving 2 mm accuracy at 10 meters\n• Dual Camera System: Equipped with two 2-megapixel cameras (front and bottom) featuring an 83.4° field of view to assist with visual positioning\n• IMU & Tilt Surveying: Utilizes advanced tilt sensor technology to support dynamic tilt surveying up to 60°, maintaining an accuracy of ≤2 cm\n• Battery Life: Powered by a 13,600 mAh battery that provides up to 20 hours of static operation, 16 hours as a rover, and 10 hours as a base\n• Rugged Construction: Housed in a magnesium-aluminum alloy shell that is IP68 waterproof and dustproof, and designed to withstand a 1.8 m pole drop\n• Connectivity: Supports comprehensive data transmission including 4G, Wi-Fi, Bluetooth V5.0, and an internal 1W radio (410-470 MHz)"
        },
        // --- SMART ANTENNAS & RECEIVERS ---
        "pulserone": {
            desc: "• Precision RTK GNSS smart antenna that combines rugged durability with cutting-edge performance.\n• Experience effortless deployment and reliable operation.\n• Tracking Total Channels 874\n  GPS L1 C/A, L1C, P1, P2, L2C, L5\n  GLONASS L1 C/A, P1, P2, L2 C/A, L3\n  Galileo E1, E5, E5A, E5B, E6\n  BeiDou B1, B1C, B2B, B2, B2A, B3\n  QZSS L1C C/A, L1C, L2C, L5, L6, L1S, L1Sb, L5S\n  SBAS L1, L5\n  NavIC L1, L5\n• GNSS+INS Firmware\n• Spoofing Detection\n• Advanced Multipath Mitigation\n• eSIM / UHF / SS Radio\n• Bluetooth & Wi-Fi\n• USB-C Interface & Power Delivery\n• Up to 7.5-hour Swappable Battery\n• Pulser Lighting System"
        },
        "triumph1mplus": {
            desc: "• Precision GNSS Smart Antenna featuring integrated wireless communications and optional MEMS IMU to deliver Tilt Compensated RTK.\n• With a full band UHF radio and a 4G cell modem, users have Base/Rover or network RTK on demand.\n• Tracking Total Channels 874\n  GPS L1 C/A, L1C, P1, P2, L2C, L5\n  GLONASS L1 C/A, P1, P2, L2 C/A, L3\n  Galileo E1, E5, E5A, E5B, E6\n  BeiDou B1, B1C, B2B, B2, B2A, B3\n  QZSS L1C C/A, L1C, L2C, L5, L6, L1S, L1Sb, L5S\n  SBAS L1, L5\n  NavIC L1, L5\n• All Constellations Activated\n• GNSS & MEMS IMU\n• 4G Cellular Modem\n• UHF Radio\n• Bluetooth & WIFI\n• Patented Pole-Secured UHF/Cell Antenna\n• 18 Hour All-Day Battery Life"
        },
        "triumph3nr": {
            desc: "• Small, lightweight, and powerful GNSS Network Rover with an integrated MEMS IMU designed for a full day of fieldwork.\n• With 25 hours of run time on a single charge, the TRIUMPH-3NR provides all-day operation without needing a battery swap or recharge.\n• Tracking Total Channels 874\n  GPS L1 C/A, L1C, P1, P2, L2C, L5\n  GLONASS L1 C/A, P1, P2, L2 C/A, L3\n  Galileo E1, E5, E5A, E5B, E6\n  BeiDou B1, B1C, B2B, B2, B2A, B3\n  QZSS L1C C/A, L1C, L2C, L5, L6, L1S, L1Sb, L5S\n  SBAS L1, L5\n  NavIC L1, L5\n• GNSS & MEMS IMU\n• All Constellations Activated\n• Small Size & Lightweight\n• 25-Hour Battery Life\n• Bluetooth, WiFi, USB\n• LED Status"
        },
        "triumph1m": {
            desc: "• Advanced GNSS Smart Antenna based on the 864-channel ASIC with expanded signal tracking.\n• Equipped with a 4G LTE cellular modem, easily accessible SD and SIM cards, and ‘Lift & Tilt’ automation.\n• Number of Channels 864\n  GPS L1 C/A, L1C (P+D), P2, L2C (L+M), L5 (I+Q)\n  GLONASS L1 C/A, P1, P2, L2C, L3 (I+Q)\n  Galileo E1 (B+C), E5A (I+Q), E5B (I+Q), AltBoc\n  BeiDou B1, B1C(P+D), B5A(I+Q), B2, B5B(I+Q)\n  QZSS L1 C/A, L1C(P+D), L1S, L2C(L+M), L5(I+Q)\n  SBAS L1, L5\n  IRNSS L5"
        },
        "sigma": {
            desc: "• Versatile receiver designed for multiple applications that require RTK.\n• Tracking Total Channels 874\n  GPS L1 C/A, L1C, P1, P2, L2C, L5\n  GLONASS L1 C/A, P1, P2, L2 C/A, L3\n  Galileo E1, E5, E5A, E5B, E6\n  BeiDou B1, B1C, B2B, B2, B2A, B3\n  QZSS L1C C/A, L1C, L2C, L5, L6, L1S, L1Sb, L5S\n  SBAS L1, L5\n  NavIC L1, L5\n  L-Band 1525-1560 Mhz.\n• Options for GNSS Heading & IMU.\n• NTRIP Caster / Server functions to transmit RTCM corrections.\n• Integrated Cell & Radio communications.\n• Ethernet, USB, Serial, Wi-Fi, Bluetooth, CAN, Event, 1PPS.\n• Performance: RTK 0.008 + 1 ppm (H), 0.015 + 1 ppm (V)\n  Network RTK 0.008 + 0.5 ppm (H), 0.015 + 0.5 ppm (V)\n  Static / Fast Static 0.003 + 0.1 ppm (H), 0.004 + 0.4 ppm (V)\n  Heading < 0.09 deg (2m basline)\n  JStar (PPP) 0.025 (H), 0.050 (V)"
        },
        "delta3s": {
            desc: "• Multi-purpose high-precision GNSS receiver architecture.\n• 874 channels supporting all constellations (GPS, GLONASS, Galileo, BeiDou, QZSS, SBAS, NavIC).\n• Advanced interference monitoring, mitigation, and spectrum analysis.\n• High-accuracy RTK positioning (8 mm + 1 ppm horizontal).\n• Fast RTK initialization time (typically 2 to 6 seconds).\n• Internal memory capacity up to 64 GB for static/kinematic logging.\n• Dual power inputs (10-30V DC) with internal rechargeable battery (18+ hrs).\n• Robust connectivity: USB, Serial, Bluetooth, and optional cellular modem.\n• Rugged IP67 environmental protection against dust and water immersion.\n• Compliant with MIL-STD-810H standards for extreme shock and vibration."
        },
        // --- DATA COLLECTION ---
        "victor4": {
            desc: "• Rugged mobile Android 14 tablet designed specifically for data collection with JAVAD GNSS receivers.\n• 8” Multi-Touch Screen (1280 x 720 HD IPS) with 700 nits brightness.\n• Dual Core 2.2 GHz + Hexa Core 2.0 GHz processor.\n• 8 GB RAM and 128 GB ROM with microSD support up to 128 GB.\n• 4G LTE Advanced cell modem, Bluetooth 5.2, and Wi-Fi 802.11 a/b/g/n/ac.\n• Built-in 13 MP Rear Camera (Auto Focus with Flash) and 5 MP Front Camera.\n• IP67 sealing with 1.22 m multi-drop resistance to concrete.\n• Runs JAVAD Mobile Tools for RTK, real-time positions, and raw data logging."
        },
        "victora4": {
            desc: "• Ultra-rugged ergonomic field computer optimized for extreme environments.\n• Wet-touch capacitive screen with chemically-strengthened Gorilla© Glass 5.\n• 5G cellular connectivity with 4G LTE fallback.\n• Runs Android 14 (supports upgrades through Android 18).\n• GMS certified using EDLA.\n• Exceptional 20-hour battery life with power-efficient processor.\n• Dual-band GPS, GLONASS, Beidou, Galileo, and QZSS support.\n• Supports wireless keyboard accessory for enhanced field data entry."
        },
        // --- PRECISION ANTENNAS ---
        "grant3l": {
            desc: "• Wide-band antenna with full GNSS spectrum compatibility.\n• Features a stable phase center with enhanced signal reception and is ideal for high precision positioning using L-Band corrections.\n• With a durable IP68 housing, the GrAnt-3L is suitable for a wide variety of applications.\n• Tracking Constellations:\n  GPS L1/L2/L5\n  GLONASS L1/L2/L3\n  GALILEO E1/E5a/E5b/E6\n  BEIDOU B1I/B1C/B2/B2a/B2b/B3\n  QZSS L1/L2/L5/L6\n  SBAS L1/L5\n  IRNSS L1/L5"
        },
        "grant3ls": {
            desc: "• Wide-band antenna with full GNSS spectrum compatibility.\n• Features a stable phase center with enhanced signal reception and is ideal for high precision positioning using L-Band corrections.\n• With a durable IP68 housing, the GrAnt-3L is suitable for a wide variety of applications.\n• Tracking Constellations:\n  GPS L1/L2/L5\n  GLONASS L1/L2/L3\n  GALILEO E1/E5a/E5b/E6\n  BEIDOU B1I/B1C/B2/B2a/B2b/B3\n  QZSS L1/L2/L5/L6\n  SBAS L1/L5\n  IRNSS L1/L5/S"
        },
        "ringantdmt": {
            desc: "• Choke ring antenna that embeds the unique Vera-Phase® technology from Tallysman.\n• Less than 1 mm Phase Center Variation and low axial ratios, well suited for precision applications such as GNSS reference networks, infrastructure monitoring, geodetic surveying, and machine control.\n• GNSS Constellations:\n  GPS L1, L2, L5\n  GLONASS L1, L2, L3\n  GALILEO E1, E5a, E5b, E6\n  BeiDou B1, B2, B2a, B3\n  QZSS L1, L2, L5, L6\n  SBAS L1, L5\n  NavIC L1, L5\n  L-Band 1539 - 1559 MHz"
        },
        "ringant3l": {
            desc: "• Precision choke-ring GNSS antenna designed to provide maximum multipath suppression and phase-center stability for reference station applications.\n• Features a rugged choke-ring structure and a side-mounted TNC connector (N-type optional).\n• GNSS Constellations:\n  GPS-L1/L2/L2C/L5\n  GLONASS L1/L2/L3\n  GALILEO E1/E2/E5ab/E6\n  BEIDOU B1/B2/B3\n  QZSS L1/L2/L2C/L5/LEX\n  WAAS L1/L5, EGNOS, MSAS, GAGAN\n  IRNSS L1/L5\n  L-Band"
        },
        "ringants": {
            desc: "• Wideband choke-ring antenna with full GNSS spectrum compatibility.\n• Features a stable phase center with enhanced signal reception and is ideal for high accuracy positioning using L-Band corrections.\n• With a durable IP68 housing, the RingAnt-S is suitable for a wide variety of precision applications.\n• Tracking Constellations:\n  GPS-L1/ L2 / L5\n  GLONASS-L1/L2 / L3\n  Galileo-E1/E5A / E5B / E6\n  BeiDou-B1 / B1C/B2A / B2B / B3\n  QZSS L1/L2 / L5 / L6\n  SBAS L1/L5\n  NavIC L1 / L5 / S-Band"
        },
        // --- OEM GNSS BOARDS ---
        "tr3s": {
            desc: "• Small-sized OEM GNSS board with 874 channels for all-in-view tracking.\n• Support for GPS, GLONASS, Galileo, BeiDou, QZSS, SBAS, IRNSS, and L-band.\n• Spoofing Detection and Advanced Multipath Mitigation.\n• Up to 200 Hz Output and 16 GB On Board Storage.\n• Configured using JAVAD's NetView software or line commands.\n• Compliance with MIL-STD-810G for shock and vibration."
        },
        "tr3sduo": {
            desc: "• 874 Channels, All GNSS Constellations.\n• GNSS Heading and Fast Acquisition Channels.\n• Spoofing & Jamming Detection and Advanced Multipath Mitigation.\n• Up to 100 Hz Output.\n• CAN, IRIG, Event Mark, 1PPS.\n• 16 GB Storage."
        },
        "tre3s": {
            desc: "• Advanced OEM GNSS Board in the TRE Family.\n• Two high speed RS232/RS422 serial ports (up to 460.8 Kbps).\n• Full-duplex 10BASE-T/100BASE-TX Ethernet port & USB 2.0.\n• Two CAN 2.0 A/B ports, IRIG timecode output, 1-PPS outputs.\n• Up to 200 Hz Update Rate and RTK Rate."
        },
        "trequattro": {
            desc: "• Advanced OEM GNSS board in the TRE Family.\n• High speed USB 2.0, Ethernet, CAN 2.0 A/B, IRIG timecode, 1-PPS outputs.\n• Up to 100 Hz Update Rate raw data (code and carrier)."
        },
        "treduoimu": {
            desc: "• All-constellation OEM GNSS receiver with dual antenna GNSS Heading and integrated MEMS IMU.\n• GNSS Heading & IMU Roll / Pitch.\n• NTRIP Caster / Server functionality.\n• Spoofing & Jamming Detection.\n• Ethernet, USB, Serial, CAN & Event, 1PPS & IRIG.\n• Advanced Multipath Rejection."
        },
        // --- OEM INS SOLUTIONS ---
        "tr2s_ins": {
            desc: "• Small, advanced OEM GNSS-aided Inertial Navigation System.\n• Combines GNSS and INS technologies.\n• Footprint suitable for any application requiring precise, uninterrupted navigation and attitude within a compact size.\n• Accelerometers and gyroscopes fully calibrated and mathematically aligned to an orthogonal coordinate system."
        },
        "tr2s_hda_ins": {
            desc: "• Small, advanced OEM GNSS-aided Inertial Navigation System.\n• Footprint suitable for high dynamics navigation and attitude within a compact size.\n• GNSS + INS Integration.\n• 874 Channels, All GNSS Tracking.\n• Spoofing & Jamming Detection.\n• Full attitude determination.\n• IPC Class 3 Electronics.\n• Small Size & Light Weight."
        },
        "tr2s_aj_ins": {
            desc: "• GNSS-aided Inertial Navigation System with advanced anti-jamming capabilities.\n• Engineered to hold position and attitude fix through signal outages, jamming, and the dynamics of flight."
        },
        "tr3s_duo_ins": {
            desc: "• Small, advanced OEM GNSS-aided Inertial Navigation System (Dual Antenna).\n• GNSS + INS Integration.\n• All GNSS Constellations.\n• Spoofing & Jamming Detection.\n• Fast Acquisition Channels.\n• Full attitude determination.\n• Small Size & Light weight."
        },
        // --- INS ENCLOSURES ---
        "alpha_ins": {
            desc: "• Advanced GNSS-aided Inertial Navigation System in a rugged environmental enclosure.\n• Available in single and dual antenna options.\n• Accelerometers and gyroscopes fully calibrated and mathematically aligned.\n• TriPad interface (two LEDs, ON/OFF, and function buttons) and Bluetooth.\n• RS232 Serial Port, USB port, Up to 16 GB eMMC memory.\n• Accepts +4.5 to +40 volts power supply."
        },
        "tau_series": {
            desc: "• INS Enclosure housing TR series OEM boards plus an IMU.\n• High-Precision GNSS+IMU solutions for easy integration in industrial and marine applications."
        },
        "theta_series": {
            desc: "• INS Enclosure housing TR series OEM boards plus an IMU.\n• Precision integration solution designed for demanding environments requiring external antennas."
        },
        // --- OEM RADIOS ---
        "fh915": {
            desc: "• High-precision OEM GNSS radio module.\n• Spread Spectrum radio data link designed for operation in harsh conditions.\n• Easily configurable for wireless capabilities in space confined applications."
        },
        "hpt401s": {
            desc: "• High-precision OEM GNSS radio module.\n• Wireless UHF data radio designed for operation in harsh conditions.\n• Provides flexible configuration options and rugged reliability for RTK."
        },
        "lmr400": {
            desc: "• High-precision OEM GNSS radio module.\n• Provides flexible configuration options and rugged reliability for data links.\n• Easily configurable and offer wireless capabilities in space confined applications."
        },
        // --- SOFTWARE ---
        "jdc": {
            desc: "• JAVAD Data Collector (JDC) Android application optimized for repeatable connection and configuration.\n• Incorporates COGO and Survey routines into the map screen for quick access and increased productivity.\n• Features a Dynamic Status Bar, Simple Configuration, and Tilt Compensation.\n• Supports Datum & Projections (including EPSG), Corrections, and Online Basemaps.\n• Automatically manages point field data for easy import and export as well as raw data logging."
        },
        "jmt": {
            desc: "• JAVAD Mobile Tools (JMT) Android data collection software.\n• Connects JAVAD GNSS receivers to Android devices via Bluetooth® or Wi-Fi.\n• Simple, intuitive interface with popular COGO routines to increase productivity.\n• Manages raw data logging and configures Base / Rover / Static RTK.\n• Includes tools for Geoid Models, Store & Stake Points, Datums & Projections, and Setup & Status.\n• Supports online basemaps and coordinates system transformations."
        },
        "netview": {
            desc: "• Windows application for easy configuration and status of JAVAD GNSS products.\n• Satellite display: total number and status of all visible and tracked satellites, skyplot, orientation plots.\n• PVT display: real-time position, velocity, time and measurements.\n• Configuration by graphical user interface or by command line.\n• Firmware Update: online from website or from a file."
        },
        "justin": {
            desc: "• Combines high performance, flexibility for post-processing GNSS observations with GIS interface and features.\n• Baseline and trajectory (static, kinematic, stop&go) post-processing.\n• Networks adjustment up to 3000 sites.\n• Import GNSS data (JAVAD.jps, RINEX, Hatanaka compressed, RTCM 3.0, CORS/SOPAC.apr, ANTEX.atx).\n• Cartographic window (projection, position, zooming, panning, scaling, ruler) and layer control."
        },
        // --- CUSTOM ---
        "custom": {
            desc: "• Customized product model configuration tailored to specific project requirements.\n• Fully adaptable technical parameters and hardware specifications.\n• Scalable performance tiers based on project scope."
        }
    };

    function formatINR(num) {
        return 'Rs. ' + num.toLocaleString('en-IN', { minimumFractionDigits: 2, maximumFractionDigits: 2 });
    }

    function onProductSelect(selectElement) {
        let row = selectElement.closest('tr');
        let selectedKey = selectElement.value;
        let product = productDatabase[selectedKey];

        if (product) {
            row.querySelector('.editable-desc').innerText = product.desc;
            calculateTotals();
        }
    }

    function addNewRow(initialSelect = "foif_a90") {
        let tbody = document.getElementById('itemsTableBody');
        let newRow = document.createElement('tr');
        
        newRow.innerHTML = `
            <td class="row-num"></td>
            <td>
                <select class="model-select" onchange="onProductSelect(this)">
                    <optgroup label="--- FOIF Products ---">
                        <option value="foif_a90">FOIF A90 GNSS Receiver</option>
                        <option value="foif_a66max">FOIF A66 Max Laser GNSS Receiver</option>
                    </optgroup>
                    <optgroup label="--- Smart Antennas & Receivers ---">
                        <option value="pulserone">PulserOne Smart Antenna</option>
                        <option value="triumph1mplus">TRIUMPH-1M Plus</option>
                        <option value="triumph3nr">TRIUMPH-3NR Network Rover</option>
                        <option value="triumph1m">TRIUMPH-1M</option>
                        <option value="sigma">SIGMA Receiver</option>
                        <option value="delta3s">DELTA-3S Receiver</option>
                    </optgroup>
                    <optgroup label="--- Data Collection ---">
                        <option value="victor4">Victor-4 Tablet</option>
                        <option value="victora4">Victor-A4 Rugged Field Computer</option>
                    </optgroup>
                    <optgroup label="--- Precision Antennas ---">
                        <option value="grant3l">GrAnt-3L Antenna</option>
                        <option value="grant3ls">GrAnt-3LS Antenna</option>
                        <option value="ringantdmt">RingAnt-DMT Choke-Ring</option>
                        <option value="ringant3l">RingAnt-3L Choke-Ring</option>
                        <option value="ringants">RingAnt-S Choke-Ring</option>
                    </optgroup>
                    <optgroup label="--- OEM GNSS Boards ---">
                        <option value="tr3s">TR-3S OEM GNSS Board</option>
                        <option value="tr3sduo">TR-3S DUO OEM GNSS Board</option>
                        <option value="tre3s">TRE-3S OEM GNSS Board</option>
                        <option value="trequattro">TRE-Quattro OEM Board</option>
                        <option value="treduoimu">TRE-DUO-IMU GNSS Board</option>
                    </optgroup>
                    <optgroup label="--- OEM INS Solutions ---">
                        <option value="tr2s_ins">TR-2S INS</option>
                        <option value="tr2s_hda_ins">TR-2S HDA INS</option>
                        <option value="tr2s_aj_ins">TR-2S AJ INS</option>
                        <option value="tr3s_duo_ins">TR-3S DUO INS</option>
                    </optgroup>
                    <optgroup label="--- INS Enclosures ---">
                        <option value="alpha_ins">ALPHA INS Enclosure</option>
                        <option value="tau_series">TAU Series INS Enclosure</option>
                        <option value="theta_series">THETA Series INS Enclosure</option>
                    </optgroup>
                    <optgroup label="--- OEM Radios ---">
                        <option value="fh915">FH915 OEM Radio</option>
                        <option value="hpt401s">HPT401S OEM Radio</option>
                        <option value="lmr400">LMR400 OEM Radio</option>
                    </optgroup>
                    <optgroup label="--- Software ---">
                        <option value="jdc">JAVAD Data Collector (JDC) App</option>
                        <option value="jmt">JAVAD Mobile Tools (JMT) App</option>
                        <option value="netview">NetView Software</option>
                        <option value="justin">Justin Post-Processing Software</option>
                    </optgroup>
                    <optgroup label="--- Custom Options ---">
                        <option value="custom">-- Custom Product / Manual Entry --</option>
                    </optgroup>
                </select>
                <div class="editable-input editable-desc" contenteditable="true"></div>
            </td>
            <td class="text-right">Rs. <input type="text" class="editable-input editable-num price-input" value="0.00" oninput="calculateTotals()"></td>
            <td class="text-right item-total">Rs. 0.00</td>
            <td class="text-center no-print"><button class="delete-btn" onclick="removeRow(this)">X</button></td>
        `;
        
        tbody.appendChild(newRow);
        
        let select = newRow.querySelector('.model-select');
        select.value = initialSelect;
        onProductSelect(select);
        updateRowNumbers();
    }

    function removeRow(btn) {
        let row = btn.closest('tr');
        row.remove();
        updateRowNumbers();
        calculateTotals();
    }

    function updateRowNumbers() {
        let rows = document.querySelectorAll('#itemsTableBody tr');
        rows.forEach((row, index) => {
            row.querySelector('.row-num').innerText = index + 1;
        });
    }

    function calculateTotals() {
        let priceInputs = document.querySelectorAll('.price-input');
        let totalSum = 0;

        priceInputs.forEach((input) => {
            let rawValue = input.value.replace(/,/g, '');
            let val = parseFloat(rawValue) || 0;
            
            let row = input.closest('tr');
            row.querySelector('.item-total').innerText = formatINR(val);
            totalSum += val;
        });

        document.getElementById('subtotal').innerText = formatINR(totalSum);
        
        let gst = totalSum * 0.18;
        document.getElementById('gstAmount').innerText = formatINR(gst);

        let gTotal = totalSum + gst;
        document.getElementById('grandTotal').innerText = formatINR(gTotal);
    }
    
    // Initial setup on load
    window.onload = function() {
        addNewRow('foif_a90');
    };
</script>

</body>
</html>
