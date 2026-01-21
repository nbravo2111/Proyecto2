# Proyecto2
Codigo HTLM
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Costos - VENCEMENT C.A.</title>
    
    <!-- Bootstrap 5 CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <!-- jsPDF -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.28/jspdf.plugin.autotable.min.js"></script>
    
    <!-- SheetJS -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #e74c3c;
            --production-color: #27ae60;
            --configuration-color: #8e44ad;
            --services-color: #f39c12;
            --taxes-color: #16a085;
            --reports-color: #9b59b6;
            --warehouse-color: #34495e;
            --fixed-assets-color: #1abc9c;
            --purchases-color: #e67e22;
            --payables-color: #d35400;
            --light-bg: #f8f9fa;
            --dark-bg: #343a40;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f5f7fa;
            color: #333;
            padding-top: 20px;
            padding-bottom: 40px;
        }
        
        .header {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            color: white;
            padding: 2rem 1rem;
            border-radius: 10px;
            margin-bottom: 2rem;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        
        .header h1 {
            font-weight: 700;
            margin-bottom: 0.5rem;
        }
        
        .stat-card {
            border-radius: 10px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            transition: transform 0.3s, box-shadow 0.3s;
            height: 100%;
            border: none;
            box-shadow: 0 4px 8px rgba(0,0,0,0.05);
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 16px rgba(0,0,0,0.1);
        }
        
        .card {
            border-radius: 10px;
            border: none;
            box-shadow: 0 4px 8px rgba(0,0,0,0.05);
            margin-bottom: 1.5rem;
        }
        
        .card-header {
            font-weight: 600;
            border-radius: 10px 10px 0 0 !important;
            padding: 1rem 1.25rem;
            border: none;
        }
        
        .card-header.produccion {
            background-color: var(--production-color);
            color: white;
        }
        
        .card-header.configuracion {
            background-color: var(--configuration-color);
            color: white;
        }
        
        .card-header.servicios {
            background-color: var(--services-color);
            color: white;
        }
        
        .card-header.impuestos {
            background-color: var(--taxes-color);
            color: white;
        }
        
        .card-header.reportes {
            background-color: var(--reports-color);
            color: white;
        }
        
        .card-header.almacen {
            background-color: var(--warehouse-color);
            color: white;
        }
        
        .card-header.activos {
            background-color: var(--fixed-assets-color);
            color: white;
        }
        
        .card-header.compras {
            background-color: var(--purchases-color);
            color: white;
        }
        
        .card-header.cuentas-pagar {
            background-color: var(--payables-color);
            color: white;
        }
        
        .table th {
            font-weight: 600;
            color: var(--primary-color);
            border-top: none;
            border-bottom: 2px solid #dee2e6;
        }
        
        .badge {
            font-weight: 500;
            padding: 0.35em 0.65em;
        }
        
        .search-box {
            position: relative;
        }
        
        .search-box .form-control {
            padding-left: 2.5rem;
            border-radius: 20px;
        }
        
        .search-box .search-icon {
            position: absolute;
            left: 1rem;
            top: 50%;
            transform: translateY(-50%);
            color: #6c757d;
        }
        
        .nav-tabs {
            border-bottom: 2px solid #dee2e6;
        }
        
        .nav-tabs .nav-link.active {
            color: var(--primary-color);
            background-color: transparent;
            border-bottom: 3px solid var(--secondary-color);
        }
        
        .nav-tabs .nav-link.active.produccion-tab {
            border-bottom-color: var(--production-color);
        }
        
        .nav-tabs .nav-link.active.configuracion-tab {
            border-bottom-color: var(--configuration-color);
        }
        
        .nav-tabs .nav-link.active.servicios-tab {
            border-bottom-color: var(--services-color);
        }
        
        .nav-tabs .nav-link.active.impuestos-tab {
            border-bottom-color: var(--taxes-color);
        }
        
        .nav-tabs .nav-link.active.reportes-tab {
            border-bottom-color: var(--reports-color);
        }
        
        .nav-tabs .nav-link.active.almacen-tab {
            border-bottom-color: var(--warehouse-color);
        }
        
        .nav-tabs .nav-link.active.activos-tab {
            border-bottom-color: var(--fixed-assets-color);
        }
        
        .nav-tabs .nav-link.active.compras-tab {
            border-bottom-color: var(--purchases-color);
        }
        
        .nav-tabs .nav-link.active.cuentas-pagar-tab {
            border-bottom-color: var(--payables-color);
        }
        
        .modal-header {
            background-color: var(--primary-color);
            color: white;
            border-radius: 10px 10px 0 0;
        }
        
        .btn-primary {
            background-color: var(--secondary-color);
            border-color: var(--secondary-color);
        }
        
        .btn-primary:hover {
            background-color: #2980b9;
            border-color: #2980b9;
        }
        
        .btn-produccion {
            background-color: var(--production-color);
            border-color: var(--production-color);
            color: white;
        }
        
        .btn-produccion:hover {
            background-color: #219653;
            border-color: #219653;
        }
        
        .btn-configuracion {
            background-color: var(--configuration-color);
            border-color: var(--configuration-color);
            color: white;
        }
        
        .btn-configuracion:hover {
            background-color: #7d3c98;
            border-color: #7d3c98;
        }
        
        .btn-servicios {
            background-color: var(--services-color);
            border-color: var(--services-color);
            color: white;
        }
        
        .btn-servicios:hover {
            background-color: #e67e22;
            border-color: #e67e22;
        }
        
        .btn-impuestos {
            background-color: var(--taxes-color);
            border-color: var(--taxes-color);
            color: white;
        }
        
        .btn-impuestos:hover {
            background-color: #138a72;
            border-color: #138a72;
        }
        
        .btn-reportes {
            background-color: var(--reports-color);
            border-color: var(--reports-color);
            color: white;
        }
        
        .btn-reportes:hover {
            background-color: #8e44ad;
            border-color: #8e44ad;
        }
        
        .btn-almacen {
            background-color: var(--warehouse-color);
            border-color: var(--warehouse-color);
            color: white;
        }
        
        .btn-almacen:hover {
            background-color: #2c3e50;
            border-color: #2c3e50;
        }
        
        .btn-activos {
            background-color: var(--fixed-assets-color);
            border-color: var(--fixed-assets-color);
            color: white;
        }
        
        .btn-activos:hover {
            background-color: #16a085;
            border-color: #16a085;
        }
        
        .btn-compras {
            background-color: var(--purchases-color);
            border-color: var(--purchases-color);
            color: white;
        }
        
        .btn-compras:hover {
            background-color: #d35400;
            border-color: #d35400;
        }
        
        .btn-cuentas-pagar {
            background-color: var(--payables-color);
            border-color: var(--payables-color);
            color: white;
        }
        
        .btn-cuentas-pagar:hover {
            background-color: #c0392b;
            border-color: #c0392b;
        }
        
        .sidebar-actions {
            position: sticky;
            top: 20px;
        }
        
        .footer {
            margin-top: 3rem;
            padding-top: 1.5rem;
            border-top: 1px solid #dee2e6;
            color: #6c757d;
            font-size: 0.9rem;
        }
        
        .input-group-currency {
            width: 100px;
        }
        
        .metric-value {
            font-weight: 600;
            font-size: 1.1rem;
        }
        
        .metric-unit {
            font-size: 0.9rem;
            color: #6c757d;
        }
        
        .section-title {
            border-left: 4px solid var(--production-color);
            padding-left: 15px;
            margin: 25px 0 15px 0;
        }
        
        .section-title-servicios {
            border-left: 4px solid var(--services-color);
        }
        
        .section-title-impuestos {
            border-left: 4px solid var(--taxes-color);
        }
        
        .section-title-reportes {
            border-left: 4px solid var(--reports-color);
        }
        
        .currency-badge {
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            color: #495057;
            font-size: 0.8rem;
        }
        
        .tasa-bcv-card {
            background: linear-gradient(135deg, #ffd166 0%, #ffb347 100%);
            color: #333;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
        }
        
        .explosivos-table {
            font-size: 0.85rem;
        }
        
        .explosivos-table th {
            font-size: 0.8rem;
        }
        
        .total-row {
            font-weight: bold;
            background-color: #f8f9fa;
        }
        
        .cantera-badge {
            background-color: #8e44ad;
            color: white;
        }
        
        .planta-badge {
            background-color: #3498db;
            color: white;
        }
        
        .formula-display {
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 5px;
            padding: 10px;
            margin: 10px 0;
            font-family: 'Courier New', monospace;
        }
        
        .alert-deadline {
            border-left: 4px solid #e74c3c;
        }
        
        .chart-container {
            position: relative;
            height: 300px;
            margin-bottom: 20px;
        }
        
        .periodo-badge {
            font-size: 0.75rem;
            margin-right: 5px;
            margin-bottom: 5px;
        }
        
        .periodo-abierto {
            background-color: #28a745 !important;
        }
        
        .periodo-cerrado {
            background-color: #dc3545 !important;
        }
        
        .periodo-pendiente {
            background-color: #ffc107 !important;
            color: #212529 !important;
        }
        
        .heatmap-cell {
            padding: 8px;
            text-align: center;
            border-radius: 4px;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        .heatmap-cell:hover {
            transform: scale(1.05);
        }
        
        .kardex-table {
            font-size: 0.8rem;
        }
        
        .depreciation-table {
            font-size: 0.85rem;
        }
        
        .movimiento-entrada {
            background-color: rgba(40, 167, 69, 0.1);
        }
        
        .movimiento-salida {
            background-color: rgba(220, 53, 69, 0.1);
        }
        
        .movimiento-ajuste {
            background-color: rgba(255, 193, 7, 0.1);
        }
        
        .asset-card {
            border: 2px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            transition: all 0.3s;
        }
        
        .asset-card:hover {
            border-color: var(--fixed-assets-color);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        .provider-card {
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 10px;
            margin-bottom: 10px;
            background-color: #f8f9fa;
        }
        
        .preview-icon {
            cursor: pointer;
            color: #3498db;
            transition: color 0.3s;
        }
        
        .preview-icon:hover {
            color: #2980b9;
        }
        
        .order-line {
            border-left: 3px solid #3498db;
            padding-left: 10px;
            margin-bottom: 10px;
            background-color: rgba(52, 152, 219, 0.05);
        }
        
        .invoice-status {
            display: inline-block;
            padding: 3px 8px;
            border-radius: 4px;
            font-size: 0.75rem;
            font-weight: bold;
        }
        
        .status-pendiente {
            background-color: #ffc107;
            color: #212529;
        }
        
        .status-parcial {
            background-color: #17a2b8;
            color: white;
        }
        
        .status-pagada {
            background-color: #28a745;
            color: white;
        }
        
        .status-vencida {
            background-color: #dc3545;
            color: white;
        }
        
        .role-badge {
            font-size: 0.7rem;
            padding: 3px 6px;
            margin-right: 5px;
        }
        
        .log-entry {
            border-left: 3px solid #6c757d;
            padding-left: 10px;
            margin-bottom: 10px;
            font-size: 0.85rem;
        }
        
        .log-entry.created {
            border-left-color: #28a745;
        }
        
        .log-entry.updated {
            border-left-color: #17a2b8;
        }
        
        .log-entry.deleted {
            border-left-color: #dc3545;
        }
        
        .log-entry.closed {
            border-left-color: #6f42c1;
        }
        
        .stock-alert {
            background-color: rgba(220, 53, 69, 0.1);
            border: 1px solid rgba(220, 53, 69, 0.3);
            border-radius: 5px;
            padding: 10px;
            margin-bottom: 10px;
        }
        
        .efficiency-indicator {
            text-align: center;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
            background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
        }
        
        .efficiency-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary-color);
        }
        
        .efficiency-label {
            font-size: 0.9rem;
            color: #6c757d;
            margin-bottom: 5px;
        }
        
        .efficiency-trend {
            font-size: 0.8rem;
            margin-top: 5px;
        }
        
        .efficiency-trend.up {
            color: #28a745;
        }
        
        .efficiency-trend.down {
            color: #dc3545;
        }
        
        .efficiency-trend.stable {
            color: #6c757d;
        }
        
        .audit-trail {
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 5px;
            padding: 10px;
            margin-top: 10px;
            font-size: 0.8rem;
        }
        
        .month-comparison {
            border: 2px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 20px;
        }
        
        .month-comparison.better {
            border-color: #28a745;
            background-color: rgba(40, 167, 69, 0.05);
        }
        
        .month-comparison.worse {
            border-color: #dc3545;
            background-color: rgba(220, 53, 69, 0.05);
        }
        
        .month-comparison.same {
            border-color: #6c757d;
            background-color: rgba(108, 117, 125, 0.05);
        }
        
        .preview-modal {
            max-width: 800px;
        }
        
        .preview-pdf {
            width: 100%;
            height: 500px;
            border: 1px solid #dee2e6;
            border-radius: 5px;
        }
        
        .unit-cost-card {
            background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%);
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
        }
        
        .unit-cost-value {
            font-size: 1.2rem;
            font-weight: bold;
            color: #1976d2;
        }
        
        .financial-metric {
            text-align: center;
            padding: 15px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-bottom: 15px;
        }
        
        .financial-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary-color);
        }
        
        .financial-label {
            font-size: 0.9rem;
            color: #6c757d;
        }
        
        .percentage-bar {
            height: 10px;
            background-color: #e9ecef;
            border-radius: 5px;
            margin-bottom: 5px;
            overflow: hidden;
        }
        
        .percentage-fill {
            height: 100%;
            border-radius: 5px;
        }
        
        .percentage-energy { background-color: #ff6b6b; }
        .percentage-raw { background-color: #4ecdc4; }
        .percentage-services { background-color: #ffe66d; }
        .percentage-taxes { background-color: #1a535c; }
        .percentage-depreciation { background-color: #95e1d3; }
        .percentage-warehouse { background-color: #f38181; }
        .percentage-other { background-color: #aaaaaa; }
        
        .tab-submenu {
            background-color: #f8f9fa;
            border-bottom: 1px solid #dee2e6;
            padding: 10px 0;
            margin-bottom: 20px;
        }
        
        .tab-submenu .nav-link {
            color: #6c757d;
            padding: 5px 15px;
            border-radius: 20px;
            margin-right: 5px;
        }
        
        .tab-submenu .nav-link.active {
            background-color: var(--secondary-color);
            color: white;
        }
        
        .item-code {
            font-family: 'Courier New', monospace;
            background-color: #f8f9fa;
            padding: 2px 6px;
            border-radius: 3px;
            border: 1px solid #dee2e6;
            font-size: 0.85rem;
        }
        
        .data-table {
            font-size: 0.9rem;
        }
        
        .data-table th {
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .export-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        
        .period-selector {
            background-color: white;
            border: 2px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 20px;
        }
        
        .period-status {
            display: inline-block;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: bold;
            margin-left: 10px;
        }
        
        .readonly-field {
            background-color: #f8f9fa;
            pointer-events: none;
        }
        
        .correction-note {
            background-color: #fff3cd;
            border: 1px solid #ffeaa7;
            border-radius: 5px;
            padding: 10px;
            margin-bottom: 10px;
            font-size: 0.85rem;
        }
        
        .digital-signature {
            font-family: 'Courier New', monospace;
            background-color: #f8f9fa;
            padding: 5px 10px;
            border-radius: 3px;
            border: 1px dashed #6c757d;
            font-size: 0.8rem;
            word-break: break-all;
        }
        
        .hash-value {
            font-family: 'Courier New', monospace;
            color: #6c757d;
            font-size: 0.75rem;
            word-break: break-all;
        }
        
        .metadata-display {
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 5px;
            padding: 10px;
            margin-bottom: 15px;
            font-size: 0.85rem;
        }
        
        .metadata-item {
            margin-bottom: 5px;
            display: flex;
        }
        
        .metadata-label {
            font-weight: bold;
            min-width: 150px;
        }
        
        .metadata-value {
            flex-grow: 1;
        }
        
        .visualization-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .visualization-card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            padding: 15px;
            height: 100%;
        }
        
        .visualization-title {
            font-size: 1rem;
            font-weight: bold;
            margin-bottom: 15px;
            color: var(--primary-color);
            border-bottom: 2px solid #f8f9fa;
            padding-bottom: 5px;
        }
        
        .comparative-chart {
            height: 250px;
            position: relative;
        }
        
        .timeline-container {
            height: 200px;
            position: relative;
        }
        
        .heatmap-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 5px;
        }
        
        .color-scale {
            display: flex;
            justify-content: space-between;
            font-size: 0.75rem;
            margin-top: 5px;
        }
        
        .color-scale-item {
            display: flex;
            align-items: center;
        }
        
        .color-box {
            width: 15px;
            height: 15px;
            margin-right: 5px;
            border-radius: 3px;
        }
        
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            display: none;
        }
        
        .loading-spinner {
            color: white;
            font-size: 3rem;
        }
        
        .quick-action {
            margin-bottom: 10px;
        }
        
        @media (max-width: 768px) {
            .visualization-grid {
                grid-template-columns: 1fr;
            }
            
            .export-buttons {
                flex-direction: column;
            }
            
            .tab-submenu {
                overflow-x: auto;
                white-space: nowrap;
            }
            
            .metadata-item {
                flex-direction: column;
            }
            
            .metadata-label {
                min-width: auto;
                margin-bottom: 2px;
            }
        }
    </style>
</head>
<body>
    <div class="container-fluid">
        <!-- Loading Overlay -->
        <div class="loading-overlay" id="loadingOverlay">
            <div class="loading-spinner">
                <i class="fas fa-spinner fa-spin"></i>
            </div>
        </div>
        
        <!-- Header -->
        <div class="header">
            <div class="row align-items-center">
                <div class="col-md-8">
                    <h1><i class="fas fa-industry me-2"></i>Sistema de Costos Integral - VENCEMENT C.A.</h1>
                    <p class="subtitle">Gestión de costos, producción, servicios, impuestos, almacén, activos, compras y cuentas por pagar</p>
                    <div id="periodoActualBadge" class="d-inline-block"></div>
                </div>
                <div class="col-md-4 text-md-end">
                    <div class="d-flex flex-column">
                        <div id="currentDateTime" class="fs-5 fw-bold">Cargando fecha y hora...</div>
                        <div class="mt-2">
                            <span class="badge bg-success">Versión 4.0</span>
                            <span class="badge bg-warning ms-1" id="tasaBcvBadge">Tasa BCV: Cargando...</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Estadísticas principales -->
        <div class="row mb-4">
            <div class="col-md-2">
                <div class="stat-card bg-white">
                    <div class="d-flex align-items-center">
                        <div class="stat-icon text-primary me-3">
                            <i class="fas fa-building"></i>
                        </div>
                        <div>
                            <div class="stat-value" id="totalCentros">0</div>
                            <div class="stat-label">Centros</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="col-md-2">
                <div class="stat-card bg-white">
                    <div class="d-flex align-items-center">
                        <div class="stat-icon text-success me-3">
                            <i class="fas fa-list-alt"></i>
                        </div>
                        <div>
                            <div class="stat-value" id="totalElementos">0</div>
                            <div class="stat-label">Elementos</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="col-md-2">
                <div class="stat-card bg-white">
                    <div class="d-flex align-items-center">
                        <div class="stat-icon text-warning me-3">
                            <i class="fas fa-chart-pie"></i>
                        </div>
                        <div>
                            <div class="stat-value" id="totalCosto">$0.00</div>
                            <div class="stat-label">Costos</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="col-md-2">
                <div class="stat-card bg-white">
                    <div class="d-flex align-items-center">
                        <div class="stat-icon text-info me-3">
                            <i class="fas fa-cogs"></i>
                        </div>
                        <div>
                            <div class="stat-value" id="totalServicios">0</div>
                            <div class="stat-label">Servicios</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="col-md-2">
                <div class="stat-card bg-white">
                    <div class="d-flex align-items-center">
                        <div class="stat-icon text-danger me-3">
                            <i class="fas fa-file-invoice-dollar"></i>
                        </div>
                        <div>
                            <div class="stat-value" id="totalImpuestos">$0.00</div>
                            <div class="stat-label">Impuestos</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="col-md-2">
                <div class="stat-card bg-white">
                    <div class="d-flex align-items-center">
                        <div class="stat-icon text-purple me-3">
                            <i class="fas fa-warehouse"></i>
                        </div>
                        <div>
                            <div class="stat-value" id="totalAlmacen">0</div>
                            <div class="stat-label">Almacén</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="row">
            <!-- Columna principal -->
            <div class="col-lg-9">
                <!-- Pestañas principales -->
                <ul class="nav nav-tabs" id="mainTabs" role="tablist">
                    <li class="nav-item" role="presentation">
                        <button class="nav-link active" id="centros-tab" data-bs-toggle="tab" data-bs-target="#centros" type="button" role="tab">
                            <i class="fas fa-building me-2"></i>Centros
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link" id="elementos-tab" data-bs-toggle="tab" data-bs-target="#elementos" type="button" role="tab">
                            <i class="fas fa-list-alt me-2"></i>Elementos
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link produccion-tab" id="produccion-tab" data-bs-toggle="tab" data-bs-target="#produccion" type="button" role="tab">
                            <i class="fas fa-industry me-2"></i>Producción
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link servicios-tab" id="servicios-tab" data-bs-toggle="tab" data-bs-target="#servicios" type="button" role="tab">
                            <i class="fas fa-tools me-2"></i>Servicios
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link impuestos-tab" id="impuestos-tab" data-bs-toggle="tab" data-bs-target="#impuestos" type="button" role="tab">
                            <i class="fas fa-file-invoice-dollar me-2"></i>Impuestos
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link reportes-tab" id="reportes-tab" data-bs-toggle="tab" data-bs-target="#reportes" type="button" role="tab">
                            <i class="fas fa-chart-bar me-2"></i>Reportes
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link almacen-tab" id="almacen-tab" data-bs-toggle="tab" data-bs-target="#almacen" type="button" role="tab">
                            <i class="fas fa-warehouse me-2"></i>Almacén
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link activos-tab" id="activos-tab" data-bs-toggle="tab" data-bs-target="#activos" type="button" role="tab">
                            <i class="fas fa-cubes me-2"></i>Activos
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link compras-tab" id="compras-tab" data-bs-toggle="tab" data-bs-target="#compras" type="button" role="tab">
                            <i class="fas fa-shopping-cart me-2"></i>Compras
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link cuentas-pagar-tab" id="cuentas-pagar-tab" data-bs-toggle="tab" data-bs-target="#cuentas-pagar" type="button" role="tab">
                            <i class="fas fa-file-invoice me-2"></i>CxP
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link configuracion-tab" id="configuracion-tab" data-bs-toggle="tab" data-bs-target="#configuracion" type="button" role="tab">
                            <i class="fas fa-cogs me-2"></i>Configuración
                        </button>
                    </li>
                </ul>
                
                <div class="tab-content mt-3" id="mainTabsContent">
                    <!-- Pestaña de Centros de Costo -->
                    <div class="tab-pane fade show active" id="centros" role="tabpanel">
                        <div class="card">
                            <div class="card-header d-flex justify-content-between align-items-center">
                                <div>
                                    <i class="fas fa-building me-2"></i>Lista de Centros de Costo
                                </div>
                                <div>
                                    <button class="btn btn-primary btn-sm" onclick="showAddCentroModal()">
                                        <i class="fas fa-plus me-1"></i>Nuevo Centro
                                    </button>
                                </div>
                            </div>
                            <div class="card-body">
                                <div class="row mb-3">
                                    <div class="col-md-8">
                                        <div class="search-box">
                                            <i class="fas fa-search search-icon"></i>
                                            <input type="text" id="searchCentros" class="form-control" placeholder="Buscar centros...">
                                        </div>
                                    </div>
                                    <div class="col-md-4">
                                        <div class="form-check mt-2 mt-md-0">
                                            <input class="form-check-input" type="checkbox" id="filterActivosCentros">
                                            <label class="form-check-label" for="filterActivosCentros">
                                                Mostrar solo activos
                                            </label>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="table-responsive">
                                    <table class="table table-hover">
                                        <thead>
                                            <tr>
                                                <th width="15%">Código</th>
                                                <th width="25%">Nombre</th>
                                                <th width="20%">Responsable</th>
                                                <th width="10%">Estado</th>
                                                <th width="15%">Elementos</th>
                                                <th width="15%">Acciones</th>
                                            </tr>
                                        </thead>
                                        <tbody id="centrosTableBody">
                                            <!-- Los datos se cargarán aquí -->
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Elementos de Costo -->
                    <div class="tab-pane fade" id="elementos" role="tabpanel">
                        <div class="card">
                            <div class="card-header d-flex justify-content-between align-items-center">
                                <div>
                                    <i class="fas fa-list-alt me-2"></i>Lista de Elementos de Costo
                                </div>
                                <div>
                                    <button class="btn btn-success btn-sm" onclick="showAddElementoModal()">
                                        <i class="fas fa-plus me-1"></i>Nuevo Elemento
                                    </button>
                                </div>
                            </div>
                            <div class="card-body">
                                <div class="row mb-3">
                                    <div class="col-md-4">
                                        <div class="search-box">
                                            <i class="fas fa-search search-icon"></i>
                                            <input type="text" id="searchElementos" class="form-control" placeholder="Buscar elementos...">
                                        </div>
                                    </div>
                                    <div class="col-md-4">
                                        <select class="form-select" id="filterCentroElemento">
                                            <option value="">Todos los centros</option>
                                        </select>
                                    </div>
                                    <div class="col-md-4">
                                        <select class="form-select" id="filterCapa">
                                            <option value="">Todas las capas</option>
                                            <option value="Estratégico">Estratégico</option>
                                            <option value="Táctico">Táctico</option>
                                            <option value="Operativo">Operativo</option>
                                        </select>
                                    </div>
                                </div>
                                
                                <div class="table-responsive">
                                    <table class="table table-hover">
                                        <thead>
                                            <tr>
                                                <th width="12%">Código</th>
                                                <th width="25%">Nombre</th>
                                                <th width="18%">Centro</th>
                                                <th width="12%">Capa</th>
                                                <th width="15%">Costo Estimado</th>
                                                <th width="10%">Estado</th>
                                                <th width="8%">Acciones</th>
                                            </tr>
                                        </thead>
                                        <tbody id="elementosTableBody">
                                            <!-- Los datos se cargarán aquí -->
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Producción -->
                    <div class="tab-pane fade" id="produccion" role="tabpanel">
                        <!-- Submenú de Producción -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#produccion-energia">Energía</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#produccion-materias">Materias Primas</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#produccion-produccion">Producción</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#produccion-costos">Costos</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#produccion-eficiencia">Eficiencia</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#produccion-graficos">Gráficos</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Energía -->
                            <div class="tab-pane fade show active" id="produccion-energia">
                                <div class="row">
                                    <!-- Tasa BCV Actual -->
                                    <div class="col-md-12 mb-4">
                                        <div class="tasa-bcv-card">
                                            <div class="row align-items-center">
                                                <div class="col-md-8">
                                                    <h5 class="mb-1"><i class="fas fa-money-bill-wave me-2"></i>Tasa de Cambio BCV</h5>
                                                    <p class="mb-0">Última actualización: <span id="tasaBcvFecha">No configurada</span></p>
                                                </div>
                                                <div class="col-md-4 text-end">
                                                    <h3 class="mb-0" id="tasaBcvValor">0.00 Bs/$</h3>
                                                    <button class="btn btn-sm btn-warning mt-2" onclick="showConfiguracionModal()">
                                                        <i class="fas fa-edit me-1"></i>Actualizar
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Electricidad -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-bolt me-2"></i>Consumo de Electricidad (kWh)
                                            </div>
                                            <div class="card-body">
                                                <div class="mb-3">
                                                    <label class="form-label">Consumo Total (kWh)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="electricidadTotal" step="0.01" min="0" value="0" required>
                                                        <span class="input-group-text">kWh</span>
                                                    </div>
                                                    <div class="mt-2">
                                                        <label class="form-label">Costo Electricidad</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="electricidadCosto" step="0.01" min="0" value="0" required>
                                                            <select class="form-select input-group-currency" id="electricidadMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <h6 class="section-title">Distribución por Área</h6>
                                                <div class="row">
                                                    <div class="col-md-6 mb-2">
                                                        <label class="form-label">Cantera</label>
                                                        <input type="number" class="form-control" id="electricidadCantera" step="0.01" min="0" value="0" required>
                                                    </div>
                                                    <div class="col-md-6 mb-2">
                                                        <label class="form-label">Crudo 2</label>
                                                        <input type="number" class="form-control" id="electricidadCrudo2" step="0.01" min="0" value="0" required>
                                                    </div>
                                                    <div class="col-md-6 mb-2">
                                                        <label class="form-label">Horno 2</label>
                                                        <input type="number" class="form-control" id="electricidadHorno2" step="0.01" min="0" value="0" required>
                                                    </div>
                                                    <div class="col-md-6 mb-2">
                                                        <label class="form-label">Cemento</label>
                                                        <input type="number" class="form-control" id="electricidadCemento" step="0.01" min="0" value="0" required>
                                                    </div>
                                                    <div class="col-md-6 mb-2">
                                                        <label class="form-label">Cemento en Saco</label>
                                                        <input type="number" class="form-control" id="electricidadCementoSaco" step="0.01" min="0" value="0" required>
                                                    </div>
                                                    <div class="col-md-6 mb-2">
                                                        <label class="form-label">Otros</label>
                                                        <input type="number" class="form-control" id="electricidadOtros" step="0.01" min="0" value="0" required>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3 text-center">
                                                    <button class="btn btn-produccion" onclick="calcularDistribucionElectricidad()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Distribución
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Gas Natural -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-fire me-2"></i>Consumo de Gas Natural (Nm³)
                                            </div>
                                            <div class="card-body">
                                                <div class="mb-3">
                                                    <label class="form-label">Consumo Total (Nm³)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="gasNaturalTotal" step="0.01" min="0" value="0" required>
                                                        <span class="input-group-text">Nm³</span>
                                                    </div>
                                                    <div class="mt-2">
                                                        <label class="form-label">Costo Gas Natural</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="gasNaturalCosto" step="0.01" min="0" value="0" required>
                                                            <select class="form-select input-group-currency" id="gasNaturalMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <h6 class="section-title">Distribución por Proceso</h6>
                                                <div class="row">
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Consumo Horno 2</label>
                                                        <input type="number" class="form-control" id="gasNaturalHorno2" step="0.01" min="0" value="0" required>
                                                    </div>
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Consumo Crudo 2</label>
                                                        <input type="number" class="form-control" id="gasNaturalCrudo2" step="0.01" min="0" value="0" required>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3 text-center">
                                                    <button class="btn btn-produccion" onclick="calcularDistribucionGas()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Distribución
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Materias Primas -->
                            <div class="tab-pane fade" id="produccion-materias">
                                <div class="row">
                                    <!-- Materias Primas -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-mountain me-2"></i>Materias Primas
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Yeso (ton)</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="yesoToneladas" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">ton</span>
                                                        </div>
                                                        <div class="input-group mt-2">
                                                            <input type="number" class="form-control" id="yesoCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                            <select class="form-select input-group-currency" id="yesoMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Sacos (unidades)</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="sacosUnidades" step="1" min="0" value="0" required>
                                                            <span class="input-group-text">und</span>
                                                        </div>
                                                        <div class="input-group mt-2">
                                                            <input type="number" class="form-control" id="sacosCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                            <select class="form-select input-group-currency" id="sacosMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <h6 class="section-title">Caliza</h6>
                                                <div class="row">
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Caliza Volada (ton)</label>
                                                        <input type="number" class="form-control" id="calizaVolada" step="0.01" min="0" value="0" required>
                                                    </div>
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Caliza Triturada (ton)</label>
                                                        <input type="number" class="form-control" id="calizaTriturada" step="0.01" min="0" value="0" required>
                                                    </div>
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Entrada a Planta (ton)</label>
                                                        <input type="number" class="form-control" id="calizaPlanta" step="0.01" min="0" value="0" required>
                                                    </div>
                                                </div>
                                                
                                                <div class="row">
                                                    <div class="col-md-6 mt-2">
                                                        <label class="form-label">Costo Caliza Volada</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="calizaVoladaCosto" step="0.01" min="0" value="0" required>
                                                            <select class="form-select input-group-currency" id="calizaVoladaMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6 mt-2">
                                                        <label class="form-label">Costo Caliza Triturada</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="calizaTrituradaCosto" step="0.01" min="0" value="0" required>
                                                            <select class="form-select input-group-currency" id="calizaTrituradaMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <label class="form-label">Arcilla (ton)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="arcillaToneladas" step="0.01" min="0" value="0" required>
                                                        <span class="input-group-text">ton</span>
                                                    </div>
                                                    <div class="input-group mt-2">
                                                        <input type="number" class="form-control" id="arcillaCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                        <select class="form-select input-group-currency" id="arcillaMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Costos Unitarios Materias Primas -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-calculator me-2"></i>Costos Unitarios Materias Primas
                                            </div>
                                            <div class="card-body">
                                                <div class="unit-cost-card">
                                                    <h6>Costo por Tonelada</h6>
                                                    <div class="row">
                                                        <div class="col-md-6 mb-3">
                                                            <div class="efficiency-label">Caliza Volada</div>
                                                            <div class="unit-cost-value" id="costoTonCalizaVolada">$0.00</div>
                                                            <small class="text-muted">USD/ton</small>
                                                        </div>
                                                        <div class="col-md-6 mb-3">
                                                            <div class="efficiency-label">Caliza Triturada</div>
                                                            <div class="unit-cost-value" id="costoTonCalizaTriturada">$0.00</div>
                                                            <small class="text-muted">USD/ton</small>
                                                        </div>
                                                        <div class="col-md-6 mb-3">
                                                            <div class="efficiency-label">Arcilla</div>
                                                            <div class="unit-cost-value" id="costoTonArcilla">$0.00</div>
                                                            <small class="text-muted">USD/ton</small>
                                                        </div>
                                                        <div class="col-md-6 mb-3">
                                                            <div class="efficiency-label">Yeso</div>
                                                            <div class="unit-cost-value" id="costoTonYeso">$0.00</div>
                                                            <small class="text-muted">USD/ton</small>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <button class="btn btn-produccion w-100" onclick="calcularCostosUnitariosMateriasPrimas()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Costos Unitarios
                                                    </button>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Resumen de Costos</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Material</th>
                                                                    <th>Cantidad</th>
                                                                    <th>Costo Total USD</th>
                                                                    <th>Costo Unitario USD</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="resumenCostosMateriasPrimas">
                                                                <tr>
                                                                    <td colspan="4" class="text-center">No hay datos</td>
                                                                </tr>
                                                            </tbody>
                                                        </table>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Producción -->
                            <div class="tab-pane fade" id="produccion-produccion">
                                <div class="row">
                                    <!-- Producción -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-industry me-2"></i>Producción
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Clinker Producido (ton)</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="produccionClinker" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">ton</span>
                                                        </div>
                                                        <div class="input-group mt-2">
                                                            <input type="number" class="form-control" id="clinkerCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                            <select class="form-select input-group-currency" id="clinkerMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Cemento Producido (ton)</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="produccionCemento" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">ton</span>
                                                        </div>
                                                        <div class="input-group mt-2">
                                                            <input type="number" class="form-control" id="cementoCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                            <select class="form-select input-group-currency" id="cementoMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <label class="form-label">Cemento en Silo (ton)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="cementoSilo" step="0.01" min="0" value="0" required>
                                                        <span class="input-group-text">ton</span>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <div class="unit-cost-card">
                                                        <h6>Costos Unitarios de Producción</h6>
                                                        <div class="row">
                                                            <div class="col-md-6 mb-3">
                                                                <div class="efficiency-label">Costo por ton de Clinker</div>
                                                                <div class="unit-cost-value" id="costoTonClinker">$0.00</div>
                                                                <small class="text-muted">USD/ton</small>
                                                            </div>
                                                            <div class="col-md-6 mb-3">
                                                                <div class="efficiency-label">Costo por ton de Cemento</div>
                                                                <div class="unit-cost-value" id="costoTonCemento">$0.00</div>
                                                                <small class="text-muted">USD/ton</small>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4 text-center">
                                                    <button class="btn btn-produccion w-100" onclick="guardarProduccion()">
                                                        <i class="fas fa-save me-2"></i>Guardar Datos de Producción
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Indicadores de Producción -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-chart-line me-2"></i>Indicadores de Producción
                                            </div>
                                            <div class="card-body">
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Relación Clinker/Cemento</div>
                                                    <div class="efficiency-value" id="relacionClinkerCemento">0.00</div>
                                                    <small class="text-muted">ton clinker / ton cemento</small>
                                                </div>
                                                
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Consumo Caliza por Clinker</div>
                                                    <div class="efficiency-value" id="consumoCalizaClinker">0.00</div>
                                                    <small class="text-muted">ton caliza / ton clinker</small>
                                                </div>
                                                
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Consumo Yeso por Cemento</div>
                                                    <div class="efficiency-value" id="consumoYesoCemento">0.00</div>
                                                    <small class="text-muted">ton yeso / ton cemento</small>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <button class="btn btn-info w-100" onclick="calcularIndicadoresProduccion()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Indicadores
                                                    </button>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Comparativo Mes Anterior</h6>
                                                    <div id="comparativoProduccion" class="month-comparison same">
                                                        <p class="text-center mb-0">No hay datos del mes anterior para comparar</p>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Costos -->
                            <div class="tab-pane fade" id="produccion-costos">
                                <div class="row">
                                    <!-- Resumen de Costos -->
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-chart-bar me-2"></i>Resumen de Costos de Producción
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-2">
                                                        <div class="text-center p-3 border rounded">
                                                            <div class="metric-value" id="costoElectricidadTotal">$0.00</div>
                                                            <div class="metric-unit">Electricidad</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-2">
                                                        <div class="text-center p-3 border rounded">
                                                            <div class="metric-value" id="costoGasTotal">$0.00</div>
                                                            <div class="metric-unit">Gas Natural</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-2">
                                                        <div class="text-center p-3 border rounded">
                                                            <div class="metric-value" id="costoMateriasPrimas">$0.00</div>
                                                            <div class="metric-unit">Materias Primas</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-2">
                                                        <div class="text-center p-3 border rounded">
                                                            <div class="metric-value" id="costoClinkerTotal">$0.00</div>
                                                            <div class="metric-unit">Clinker</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-2">
                                                        <div class="text-center p-3 border rounded">
                                                            <div class="metric-value" id="costoCementoTotal">$0.00</div>
                                                            <div class="metric-unit">Cemento</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-2">
                                                        <div class="text-center p-3 border rounded bg-primary text-white">
                                                            <div class="metric-value" id="costoTotalProduccion">$0.00</div>
                                                            <div class="metric-unit">Total Producción</div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Participación Porcentual por Categoría</h6>
                                                    <div class="row">
                                                        <div class="col-md-8">
                                                            <div id="participacionCostosChart" class="chart-container">
                                                                <canvas id="participacionCostosCanvas"></canvas>
                                                            </div>
                                                        </div>
                                                        <div class="col-md-4">
                                                            <div class="percentage-bar">
                                                                <div class="percentage-fill percentage-energy" id="barraEnergia" style="width: 0%"></div>
                                                            </div>
                                                            <div class="d-flex justify-content-between">
                                                                <span>Energía</span>
                                                                <span id="porcentajeEnergia">0%</span>
                                                            </div>
                                                            
                                                            <div class="percentage-bar mt-2">
                                                                <div class="percentage-fill percentage-raw" id="barraMateriasPrimas" style="width: 0%"></div>
                                                            </div>
                                                            <div class="d-flex justify-content-between">
                                                                <span>Materias Primas</span>
                                                                <span id="porcentajeMateriasPrimas">0%</span>
                                                            </div>
                                                            
                                                            <div class="percentage-bar mt-2">
                                                                <div class="percentage-fill percentage-other" id="barraProcesamiento" style="width: 0%"></div>
                                                            </div>
                                                            <div class="d-flex justify-content-between">
                                                                <span>Procesamiento</span>
                                                                <span id="porcentajeProcesamiento">0%</span>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Detalle de Costos:</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Concepto</th>
                                                                    <th>Cantidad</th>
                                                                    <th>Costo USD</th>
                                                                    <th>Costo Bs</th>
                                                                    <th>Costo Unitario USD</th>
                                                                    <th>Acción</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="detalleCostosProduccion">
                                                                <tr>
                                                                    <td colspan="6" class="text-center">No hay datos calculados</td>
                                                                </tr>
                                                            </tbody>
                                                        </table>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3 text-center">
                                                    <button class="btn btn-produccion" onclick="calcularCostosProduccion()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Costos Totales
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Eficiencia -->
                            <div class="tab-pane fade" id="produccion-eficiencia">
                                <div class="row">
                                    <!-- Indicadores de Eficiencia -->
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-tachometer-alt me-2"></i>Indicadores de Eficiencia
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="efficiency-indicator">
                                                            <div class="efficiency-label">kWh/ton Clinker</div>
                                                            <div class="efficiency-value" id="kwhTonClinker">0.00</div>
                                                            <div class="efficiency-trend stable" id="tendenciaKwhClinker">
                                                                <i class="fas fa-minus"></i> Sin datos previos
                                                            </div>
                                                            <small class="text-muted">Consumo eléctrico por tonelada de clinker</small>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="efficiency-indicator">
                                                            <div class="efficiency-label">Nm³/ton Cemento</div>
                                                            <div class="efficiency-value" id="nm3TonCemento">0.00</div>
                                                            <div class="efficiency-trend stable" id="tendenciaGasCemento">
                                                                <i class="fas fa-minus"></i> Sin datos previos
                                                            </div>
                                                            <small class="text-muted">Consumo gas por tonelada de cemento</small>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="efficiency-indicator">
                                                            <div class="efficiency-label">L gasoil/ton Acarreo</div>
                                                            <div class="efficiency-value" id="gasoilTonAcarreo">0.00</div>
                                                            <div class="efficiency-trend stable" id="tendenciaGasoilAcarreo">
                                                                <i class="fas fa-minus"></i> Sin datos previos
                                                            </div>
                                                            <small class="text-muted">Consumo gasoil por tonelada acarreada</small>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-4">
                                                        <div class="efficiency-indicator">
                                                            <div class="efficiency-label">USD/ton Clinker</div>
                                                            <div class="efficiency-value" id="usdTonClinker">$0.00</div>
                                                            <div class="efficiency-trend stable" id="tendenciaCostoClinker">
                                                                <i class="fas fa-minus"></i> Sin datos previos
                                                            </div>
                                                            <small class="text-muted">Costo total por tonelada de clinker</small>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="efficiency-indicator">
                                                            <div class="efficiency-label">USD/ton Cemento</div>
                                                            <div class="efficiency-value" id="usdTonCemento">$0.00</div>
                                                            <div class="efficiency-trend stable" id="tendenciaCostoCemento">
                                                                <i class="fas fa-minus"></i> Sin datos previos
                                                            </div>
                                                            <small class="text-muted">Costo total por tonelada de cemento</small>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="efficiency-indicator">
                                                            <div class="efficiency-label">USD/saco Cemento</div>
                                                            <div class="efficiency-value" id="usdSacoCemento">$0.00</div>
                                                            <div class="efficiency-trend stable" id="tendenciaCostoSaco">
                                                                <i class="fas fa-minus"></i> Sin datos previos
                                                            </div>
                                                            <small class="text-muted">Costo por saco de cemento (42.5kg)</small>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Meta vs Real</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Indicador</th>
                                                                    <th>Meta</th>
                                                                    <th>Real</th>
                                                                    <th>Desviación</th>
                                                                    <th>Estado</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="tablaMetasEficiencia">
                                                                <tr>
                                                                    <td>kWh/ton Clinker</td>
                                                                    <td><input type="number" class="form-control form-control-sm" id="metaKwhClinker" value="110" step="0.01"></td>
                                                                    <td id="realKwhClinker">0.00</td>
                                                                    <td id="desviacionKwhClinker">0.00%</td>
                                                                    <td><span class="badge bg-secondary">Sin datos</span></td>
                                                                </tr>
                                                                <tr>
                                                                    <td>Nm³/ton Cemento</td>
                                                                    <td><input type="number" class="form-control form-control-sm" id="metaGasCemento" value="80" step="0.01"></td>
                                                                    <td id="realGasCemento">0.00</td>
                                                                    <td id="desviacionGasCemento">0.00%</td>
                                                                    <td><span class="badge bg-secondary">Sin datos</span></td>
                                                                </tr>
                                                                <tr>
                                                                    <td>USD/ton Cemento</td>
                                                                    <td><input type="number" class="form-control form-control-sm" id="metaCostoCemento" value="45" step="0.01"></td>
                                                                    <td id="realCostoCemento">$0.00</td>
                                                                    <td id="desviacionCostoCemento">0.00%</td>
                                                                    <td><span class="badge bg-secondary">Sin datos</span></td>
                                                                </tr>
                                                            </tbody>
                                                        </table>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3 text-center">
                                                    <button class="btn btn-produccion" onclick="calcularIndicadoresEficiencia()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Indicadores de Eficiencia
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Gráficos -->
                            <div class="tab-pane fade" id="produccion-graficos">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header produccion">
                                                <i class="fas fa-chart-area me-2"></i>Visualización Gráfica
                                            </div>
                                            <div class="card-body">
                                                <div class="visualization-grid">
                                                    <div class="visualization-card">
                                                        <div class="visualization-title">Distribución de Costos</div>
                                                        <div class="chart-container">
                                                            <canvas id="distribucionCostosChart"></canvas>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="visualization-card">
                                                        <div class="visualization-title">Evolución Mensual</div>
                                                        <div class="timeline-container">
                                                            <canvas id="evolucionCostosChart"></canvas>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="visualization-card">
                                                        <div class="visualization-title">Comparativo por Rubro</div>
                                                        <div class="comparative-chart">
                                                            <canvas id="comparativoRubrosChart"></canvas>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="visualization-card">
                                                        <div class="visualization-title">Heatmap de Eficiencia</div>
                                                        <div class="heatmap-container" id="heatmapEficiencia">
                                                            <!-- Heatmap se generará dinámicamente -->
                                                            <div class="text-center p-4">
                                                                <i class="fas fa-chart-bar fa-2x text-muted"></i>
                                                                <p class="mt-2">Generar datos primero</p>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3 text-center">
                                                    <button class="btn btn-produccion" onclick="generarGraficosProduccion()">
                                                        <i class="fas fa-chart-line me-2"></i>Generar Gráficos
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Servicios -->
                    <div class="tab-pane fade" id="servicios" role="tabpanel">
                        <!-- Submenú de Servicios -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#servicios-combustibles">Combustibles</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#servicios-comedor">Comedor</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#servicios-otros">Otros Servicios</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#servicios-transporte">Transporte</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#servicios-explosivos">Explosivos</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#servicios-resumen">Resumen</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Combustibles -->
                            <div class="tab-pane fade show active" id="servicios-combustibles">
                                <div class="row">
                                    <!-- Combustibles -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header servicios">
                                                <i class="fas fa-gas-pump me-2"></i>Combustibles - Gasoil
                                            </div>
                                            <div class="card-body">
                                                <h6 class="section-title section-title-servicios">Planta Ocumare</h6>
                                                <div class="row mb-3">
                                                    <div class="col-md-6">
                                                        <label class="form-label">Consumo (Litros)</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="gasoilPlantaLitros" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">L</span>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <label class="form-label">Flete</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="gasoilPlantaFlete" step="0.01" min="0" value="0" required>
                                                            <select class="form-select input-group-currency" id="gasoilPlantaMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <h6 class="section-title section-title-servicios">Cantera</h6>
                                                <div class="row mb-3">
                                                    <div class="col-md-6">
                                                        <label class="form-label">Consumo (Litros)</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="gasoilCanteraLitros" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">L</span>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <label class="form-label">Flete</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="gasoilCanteraFlete" step="0.01" min="0" value="0" required>
                                                            <select class="form-select input-group-currency" id="gasoilCanteraMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="text-center p-3 border rounded bg-light">
                                                            <div class="metric-value" id="totalGasoilLitros">0 L</div>
                                                            <div class="metric-unit">Total Gasoil</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="text-center p-3 border rounded bg-light">
                                                            <div class="metric-value" id="totalGasoilCosto">$0.00</div>
                                                            <div class="metric-unit">Total Costo</div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <button class="btn btn-servicios w-100" onclick="calcularTotalGasoil()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Total Gasoil
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Indicadores de Eficiencia Gasoil -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header servicios">
                                                <i class="fas fa-tachometer-alt me-2"></i>Indicadores de Eficiencia - Gasoil
                                            </div>
                                            <div class="card-body">
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Consumo Gasoil Planta</div>
                                                    <div class="efficiency-value" id="indicadorGasoilPlanta">0.00 L</div>
                                                    <small class="text-muted">Total consumo planta</small>
                                                </div>
                                                
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Consumo Gasoil Cantera</div>
                                                    <div class="efficiency-value" id="indicadorGasoilCantera">0.00 L</div>
                                                    <small class="text-muted">Total consumo cantera</small>
                                                </div>
                                                
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Costo por Litro (USD)</div>
                                                    <div class="efficiency-value" id="costoLitroGasoil">$0.00</div>
                                                    <small class="text-muted">Costo promedio por litro</small>
                                                </div>
                                                
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">L gasoil/ton Acarreo</div>
                                                    <div class="efficiency-value" id="gasoilTonAcarreoServicios">0.00</div>
                                                    <div class="efficiency-trend stable">
                                                        <i class="fas fa-minus"></i> Sin comparación
                                                    </div>
                                                    <small class="text-muted">Eficiencia en acarreo</small>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <button class="btn btn-info w-100" onclick="calcularIndicadoresGasoil()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Indicadores
                                                    </button>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Meta de Consumo</h6>
                                                    <div class="input-group mb-3">
                                                        <span class="input-group-text">Meta Planta</span>
                                                        <input type="number" class="form-control" id="metaGasoilPlanta" value="4000" step="0.01">
                                                        <span class="input-group-text">L</span>
                                                    </div>
                                                    <div class="input-group">
                                                        <span class="input-group-text">Meta Cantera</span>
                                                        <input type="number" class="form-control" id="metaGasoilCantera" value="2500" step="0.01">
                                                        <span class="input-group-text">L</span>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Comedor -->
                            <div class="tab-pane fade" id="servicios-comedor">
                                <div class="row">
                                    <!-- Comedor -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header servicios">
                                                <i class="fas fa-utensils me-2"></i>Comedor
                                            </div>
                                            <div class="card-body">
                                                <div class="mb-3">
                                                    <label class="form-label">Provisión Total</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="comedorProvision" step="0.01" min="0" value="0" required>
                                                        <select class="form-select input-group-currency" id="comedorMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                                
                                                <h6 class="section-title section-title-servicios">Planta Ocumare</h6>
                                                <div class="row">
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Desayuno</label>
                                                        <input type="number" class="form-control" id="comedorPlantaDesayuno" step="1" min="0" value="0" placeholder="Comensales" required>
                                                    </div>
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Almuerzo</label>
                                                        <input type="number" class="form-control" id="comedorPlantaAlmuerzo" step="1" min="0" value="0" placeholder="Comensales" required>
                                                    </div>
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Cena</label>
                                                        <input type="number" class="form-control" id="comedorPlantaCena" step="1" min="0" value="0" placeholder="Comensales" required>
                                                    </div>
                                                </div>
                                                
                                                <h6 class="section-title section-title-servicios">Cantera</h6>
                                                <div class="row">
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Desayuno</label>
                                                        <input type="number" class="form-control" id="comedorCanteraDesayuno" step="1" min="0" value="0" placeholder="Comensales" required>
                                                    </div>
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Almuerzo</label>
                                                        <input type="number" class="form-control" id="comedorCanteraAlmuerzo" step="1" min="0" value="0" placeholder="Comensales" required>
                                                    </div>
                                                    <div class="col-md-4 mb-2">
                                                        <label class="form-label">Cena</label>
                                                        <input type="number" class="form-control" id="comedorCanteraCena" step="1" min="0" value="0" placeholder="Comensales" required>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <label class="form-label">Otros (Agregar descripción)</label>
                                                    <textarea class="form-control" id="comedorOtrosDescripcion" rows="2" placeholder="Descripción de otros servicios de comedor..."></textarea>
                                                    <div class="input-group mt-2">
                                                        <input type="number" class="form-control" id="comedorOtrosMonto" step="0.01" min="0" value="0" placeholder="Monto" required>
                                                        <select class="form-select input-group-currency" id="comedorOtrosMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3 text-center">
                                                    <button class="btn btn-servicios" onclick="calcularDistribucionComedor()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Distribución
                                                    </button>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <div class="row">
                                                        <div class="col-md-6">
                                                            <div class="p-2 border rounded">
                                                                <small>Planta Ocumare</small>
                                                                <div class="metric-value" id="comedorPlantaTotal">0 comensales</div>
                                                                <div class="metric-value" id="comedorPlantaCosto">$0.00</div>
                                                            </div>
                                                        </div>
                                                        <div class="col-md-6">
                                                            <div class="p-2 border rounded">
                                                                <small>Cantera</small>
                                                                <div class="metric-value" id="comedorCanteraTotal">0 comensales</div>
                                                                <div class="metric-value" id="comedorCanteraCosto">$0.00</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Indicadores Comedor -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header servicios">
                                                <i class="fas fa-chart-pie me-2"></i>Indicadores Comedor
                                            </div>
                                            <div class="card-body">
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Costo por Comensal</div>
                                                    <div class="efficiency-value" id="costoPorComensal">$0.00</div>
                                                    <small class="text-muted">Costo promedio por comensal</small>
                                                </div>
                                                
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Total Comensales</div>
                                                    <div class="efficiency-value" id="totalComensales">0</div>
                                                    <small class="text-muted">Total de comidas servidas</small>
                                                </div>
                                                
                                                <div class="efficiency-indicator">
                                                    <div class="efficiency-label">Distribución Planta/Cantera</div>
                                                    <div class="efficiency-value" id="distribucionPlantaCantera">0%/0%</div>
                                                    <small class="text-muted">Porcentaje de distribución</small>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Análisis de Costos</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Concepto</th>
                                                                    <th>Costo USD</th>
                                                                    <th>% del Total</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="analisisCostosComedor">
                                                                <tr>
                                                                    <td colspan="3" class="text-center">No hay datos</td>
                                                                </tr>
                                                            </tbody>
                                                        </table>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <button class="btn btn-info w-100" onclick="analizarCostosComedor()">
                                                        <i class="fas fa-chart-bar me-2"></i>Analizar Costos
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Otros Servicios -->
                            <div class="tab-pane fade" id="servicios-otros">
                                <div class="row">
                                    <!-- Otros Servicios -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header servicios">
                                                <i class="fas fa-fire me-2"></i>Gas de Comedor y Otros
                                            </div>
                                            <div class="card-body">
                                                <div class="mb-3">
                                                    <label class="form-label">Gas de Comedor (Litros)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="gasComedorLitros" step="0.01" min="0" value="0" required>
                                                        <span class="input-group-text">L</span>
                                                    </div>
                                                    <div class="input-group mt-2">
                                                        <input type="number" class="form-control" id="gasComedorCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                        <select class="form-select input-group-currency" id="gasComedorMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Maquinaria Alquilada (Horas)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="maquinariaHoras" step="0.01" min="0" value="0" required>
                                                        <span class="input-group-text">hrs</span>
                                                    </div>
                                                    <div class="input-group mt-2">
                                                        <input type="number" class="form-control" id="maquinariaCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                        <select class="form-select input-group-currency" id="maquinariaMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Servicio de Telecomunicaciones</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="telecomunicacionesCosto" step="0.01" min="0" value="0" required>
                                                        <select class="form-select input-group-currency" id="telecomunicacionesMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Servicio de Perforación San Bernardo (Horas)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="perforacionHoras" step="0.01" min="0" value="0" required>
                                                        <span class="input-group-text">hrs</span>
                                                    </div>
                                                    <div class="input-group mt-2">
                                                        <input type="number" class="form-control" id="perforacionCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                        <select class="form-select input-group-currency" id="perforacionMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Servicios de Acarreo y Transporte -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header servicios">
                                                <i class="fas fa-truck me-2"></i>Acarreo y Transporte
                                            </div>
                                            <div class="card-body">
                                                <h6 class="section-title section-title-servicios">Servicios de Acarreo (Toneladas)</h6>
                                                <div class="row">
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Arcilla</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="acarreoArcilla" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">ton</span>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Caliza Externa</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="acarreoCalizaExterna" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">ton</span>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Clinker</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="acarreoClinker" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">ton</span>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Caliza Interna</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="acarreoCalizaInterna" step="0.01" min="0" value="0" required>
                                                            <span class="input-group-text">ton</span>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <div class="text-center p-3 border rounded bg-light">
                                                        <div class="metric-value" id="totalAcarreoToneladas">0 ton</div>
                                                        <div class="metric-unit">Total Acarreo</div>
                                                    </div>
                                                </div>
                                                
                                                <h6 class="section-title section-title-servicios mt-4">Transporte de Personal</h6>
                                                <div class="row">
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Planta Ocumare (Viajes)</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="transportePlantaViajes" step="1" min="0" value="0" required>
                                                            <span class="input-group-text">viajes</span>
                                                        </div>
                                                        <div class="input-group mt-2">
                                                            <input type="number" class="form-control" id="transportePlantaCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                            <select class="form-select input-group-currency" id="transportePlantaMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6 mb-3">
                                                        <label class="form-label">Cantera (Viajes)</label>
                                                        <div class="input-group">
                                                            <input type="number" class="form-control" id="transporteCanteraViajes" step="1" min="0" value="0" required>
                                                            <span class="input-group-text">viajes</span>
                                                        </div>
                                                        <div class="input-group mt-2">
                                                            <input type="number" class="form-control" id="transporteCanteraCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                            <select class="form-select input-group-currency" id="transporteCanteraMoneda">
                                                                <option value="USD">USD</option>
                                                                <option value="BS">Bs</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Servicio de Vigilancia (Oficiales)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="vigilanciaOficiales" step="1" min="0" value="0" required>
                                                        <span class="input-group-text">oficiales</span>
                                                    </div>
                                                    <div class="input-group mt-2">
                                                        <input type="number" class="form-control" id="vigilanciaCosto" step="0.01" min="0" value="0" placeholder="Costo" required>
                                                        <select class="form-select input-group-currency" id="vigilanciaMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Explosivos -->
                            <div class="tab-pane fade" id="servicios-explosivos">
                                <div class="row">
                                    <!-- Explosivos -->
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header servicios">
                                                <i class="fas fa-explosion me-2"></i>Explosivos
                                            </div>
                                            <div class="card-body">
                                                <div class="table-responsive">
                                                    <table class="table explosivos-table">
                                                        <thead>
                                                            <tr>
                                                                <th width="40%">Producto</th>
                                                                <th width="15%">Consumo (kg)</th>
                                                                <th width="15%">Precio Unitario</th>
                                                                <th width="15%">Moneda</th>
                                                                <th width="15%">Total</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaExplosivos">
                                                            <tr>
                                                                <td>
                                                                    <input type="text" class="form-control form-control-sm" value="BOOSTER MINERO PETEX 450 GR" placeholder="Producto" required>
                                                                </td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="20" placeholder="kg" required>
                                                                </td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="18.28" placeholder="PU" required>
                                                                </td>
                                                                <td>
                                                                    <select class="form-select form-select-sm">
                                                                        <option value="USD">USD</option>
                                                                        <option value="BS">Bs</option>
                                                                    </select>
                                                                </td>
                                                                <td>
                                                                    <span class="metric-value">$365.60</span>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>
                                                                    <input type="text" class="form-control form-control-sm" value="CONECTOR EXCEL" placeholder="Producto" required>
                                                                </td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="3" placeholder="kg" required>
                                                                </td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="21.27" placeholder="PU" required>
                                                                </td>
                                                                <td>
                                                                    <select class="form-select form-select-sm">
                                                                        <option value="USD">USD</option>
                                                                        <option value="BS">Bs</option>
                                                                    </select>
                                                                </td>
                                                                <td>
                                                                    <span class="metric-value">$63.81</span>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>
                                                                    <input type="text" class="form-control form-control-sm" value="DETONADOR EXCEL HANDIDET 17/350 X 60 PIE" placeholder="Producto" required>
                                                                </td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="20" placeholder="kg" required>
                                                                </td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="38.67" placeholder="PU" required>
                                                                </td>
                                                                <td>
                                                                    <select class="form-select form-select-sm">
                                                                        <option value="USD">USD</option>
                                                                        <option value="BS">Bs</option>
                                                                    </select>
                                                                </td>
                                                                <td>
                                                                    <span class="metric-value">$773.40</span>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>
                                                                    <input type="text" class="form-control form-control-sm" value="ANFO (20 KG)" placeholder="Producto" required>
                                                                </td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="45" placeholder="kg" required>
                                                                </td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="1802.10" placeholder="PU" required>
                                                                </td>
                                                                <td>
                                                                    <select class="form-select form-select-sm">
                                                                        <option value="USD">USD</option>
                                                                        <option value="BS">Bs</option>
                                                                    </select>
                                                                </td>
                                                                <td>
                                                                    <span class="metric-value">$81,094.50</span>
                                                                </td>
                                                            </tr>
                                                        </tbody>
                                                        <tfoot>
                                                            <tr class="total-row">
                                                                <td colspan="4" class="text-end"><strong>TOTAL EXPLOSIVOS:</strong></td>
                                                                <td><strong id="totalExplosivos">$82,297.31</strong></td>
                                                            </tr>
                                                        </tfoot>
                                                    </table>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <button class="btn btn-sm btn-servicios me-2" onclick="calcularExplosivos()">
                                                        <i class="fas fa-calculator me-1"></i>Calcular
                                                    </button>
                                                    <button class="btn btn-sm btn-outline-secondary" onclick="agregarFilaExplosivos()">
                                                        <i class="fas fa-plus me-1"></i>Agregar Producto
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Resumen -->
                            <div class="tab-pane fade" id="servicios-resumen">
                                <div class="row">
                                    <!-- Resumen de Servicios -->
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header servicios">
                                                <i class="fas fa-chart-bar me-2"></i>Resumen de Servicios
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-3">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenTotalServicios">$0.00</div>
                                                            <div class="financial-label">Total Servicios</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenCombustibles">$0.00</div>
                                                            <div class="financial-label">Combustibles</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenComedor">$0.00</div>
                                                            <div class="financial-label">Comedor</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenExplosivos">$0.00</div>
                                                            <div class="financial-label">Explosivos</div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Distribución de Costos por Servicio</h6>
                                                    <div class="chart-container">
                                                        <canvas id="distribucionServiciosChart"></canvas>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Detalle por Servicio</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Servicio</th>
                                                                    <th>Costo USD</th>
                                                                    <th>Costo Bs</th>
                                                                    <th>% del Total</th>
                                                                    <th>Acción</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="detalleServiciosResumen">
                                                                <tr>
                                                                    <td colspan="5" class="text-center">No hay datos</td>
                                                                </tr>
                                                            </tbody>
                                                        </table>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3 text-center">
                                                    <button class="btn btn-servicios btn-lg" onclick="guardarServicios()">
                                                        <i class="fas fa-save me-2"></i>Guardar Todos los Servicios
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Impuestos -->
                    <div class="tab-pane fade" id="impuestos" role="tabpanel">
                        <!-- Submenú de Impuestos -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#impuestos-mineros">Mineros</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#impuestos-municipales">Municipales</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#impuestos-areas">Áreas</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#impuestos-resumen">Resumen</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#impuestos-alertas">Alertas</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Mineros -->
                            <div class="tab-pane fade show active" id="impuestos-mineros">
                                <div class="row">
                                    <!-- Impuestos Mineros (IADEMIN) -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header impuestos">
                                                <i class="fas fa-mountain me-2"></i>Impuestos Mineros (IADEMIN)
                                            </div>
                                            <div class="card-body">
                                                <div class="mb-3">
                                                    <label class="form-label">Tipo de Mineral</label>
                                                    <select class="form-select" id="impuestoMineral">
                                                        <option value="Caliza">Caliza</option>
                                                        <option value="Arcilla">Arcilla</option>
                                                        <option value="Yeso">Yeso</option>
                                                        <option value="Otro">Otro</option>
                                                    </select>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Volumen Base Extraído</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="impuestoVolumen" step="0.01" min="0" value="0" required>
                                                        <select class="form-select" id="impuestoUnidad">
                                                            <option value="ton">Toneladas (ton)</option>
                                                            <option value="m3">Metros Cúbicos (m³)</option>
                                                        </select>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Precio Unitario Oficial</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="impuestoPrecioUnitario" step="0.01" min="0" value="0" required>
                                                        <span class="input-group-text">Bs/m³</span>
                                                    </div>
                                                    <small class="text-muted">Según providencia administrativa</small>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Porcentaje de Regalía (%)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="impuestoRegalia" step="0.01" min="0" max="100" value="14.95" required>
                                                        <span class="input-group-text">%</span>
                                                    </div>
                                                    <small class="text-muted">
                                                        <span id="regaliaInfo">Caliza: 14.95%</span>
                                                    </small>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Fecha Límite de Pago</label>
                                                    <input type="date" class="form-control" id="impuestoFechaLimite" required>
                                                </div>
                                                
                                                <div class="formula-display">
                                                    <strong>Fórmula:</strong><br>
                                                    <span id="formulaRegalia">Volumen × Precio Unitario × (Regalía / 100) = Impuesto en Bs</span>
                                                </div>
                                                
                                                <div class="d-grid">
                                                    <button class="btn btn-impuestos" onclick="calcularImpuestoMineros()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Impuesto Minero
                                                    </button>
                                                </div>
                                                
                                                <div class="mt-4 p-3 border rounded bg-light">
                                                    <h6>Resultado del Cálculo:</h6>
                                                    <div class="row">
                                                        <div class="col-md-6">
                                                            <small>Impuesto en Bs:</small>
                                                            <div class="metric-value" id="impuestoResultadoBs">0.00 Bs</div>
                                                        </div>
                                                        <div class="col-md-6">
                                                            <small>Impuesto en USD:</small>
                                                            <div class="metric-value" id="impuestoResultadoUsd">$0.00</div>
                                                        </div>
                                                    </div>
                                                    <div class="mt-2">
                                                        <small>Vencimiento:</small>
                                                        <div class="metric-value" id="impuestoVencimiento">--/--/----</div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Impuestos Mineros por Cantera -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header impuestos">
                                                <i class="fas fa-map-marked-alt me-2"></i>Impuestos Mineros por Cantera
                                            </div>
                                            <div class="card-body">
                                                <div class="table-responsive">
                                                    <table class="table table-sm">
                                                        <thead>
                                                            <tr>
                                                                <th>Cantera</th>
                                                                <th>Mineral</th>
                                                                <th>Volumen</th>
                                                                <th>Regalía %</th>
                                                                <th>Impuesto USD</th>
                                                                <th>Acción</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaImpuestosCanteras">
                                                            <tr>
                                                                <td>San Bernardo</td>
                                                                <td>Caliza</td>
                                                                <td>15,000 ton</td>
                                                                <td>14.95%</td>
                                                                <td>$8,450.00</td>
                                                                <td>
                                                                    <button class="btn btn-sm btn-outline-primary" onclick="editarImpuestoCantera(0)">
                                                                        <i class="fas fa-edit"></i>
                                                                    </button>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>La Cabrera</td>
                                                                <td>Caliza</td>
                                                                <td>5,000 ton</td>
                                                                <td>14.95%</td>
                                                                <td>$2,816.67</td>
                                                                <td>
                                                                    <button class="btn btn-sm btn-outline-primary" onclick="editarImpuestoCantera(1)">
                                                                        <i class="fas fa-edit"></i>
                                                                    </button>
                                                                </td>
                                                            </tr>
                                                        </tbody>
                                                        <tfoot>
                                                            <tr class="total-row">
                                                                <td colspan="4" class="text-end"><strong>TOTAL:</strong></td>
                                                                <td><strong id="totalImpuestosCanteras">$11,266.67</strong></td>
                                                                <td></td>
                                                            </tr>
                                                        </tfoot>
                                                    </table>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <button class="btn btn-sm btn-impuestos" onclick="agregarImpuestoCantera()">
                                                        <i class="fas fa-plus me-1"></i>Agregar Cantera
                                                    </button>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Configuración Mensual</h6>
                                                    <div class="input-group mb-3">
                                                        <span class="input-group-text">Mes de Pago</span>
                                                        <select class="form-select" id="mesPagoImpuestosMineros">
                                                            <option value="1">Enero</option>
                                                            <option value="2">Febrero</option>
                                                            <option value="3">Marzo</option>
                                                            <option value="4">Abril</option>
                                                            <option value="5">Mayo</option>
                                                            <option value="6">Junio</option>
                                                            <option value="7">Julio</option>
                                                            <option value="8">Agosto</option>
                                                            <option value="9">Septiembre</option>
                                                            <option value="10">Octubre</option>
                                                            <option value="11">Noviembre</option>
                                                            <option value="12">Diciembre</option>
                                                        </select>
                                                    </div>
                                                    <small class="text-muted">El impuesto minero se calcula mensualmente según el volumen extraído</small>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Municipales -->
                            <div class="tab-pane fade" id="impuestos-municipales">
                                <div class="row">
                                    <!-- Impuestos Municipales -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header impuestos">
                                                <i class="fas fa-landmark me-2"></i>Impuestos Municipales
                                            </div>
                                            <div class="card-body">
                                                <div class="mb-3">
                                                    <label class="form-label">Municipio</label>
                                                    <select class="form-select" id="impuestoMunicipio">
                                                        <option value="Tomas Lander">Tomas Lander</option>
                                                        <option value="Ocumare del Tuy">Ocumare del Tuy</option>
                                                        <option value="Independencia">Independencia</option>
                                                        <option value="Otro">Otro</option>
                                                    </select>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Sector Económico</label>
                                                    <input type="text" class="form-control" id="impuestoSector" value="Manufactura (fabricación de cemento)" readonly>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Código de Actividad Económica</label>
                                                    <input type="text" class="form-control" id="impuestoCodigo" value="2.02.02" readonly>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Ingresos Brutos Declarados</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="impuestoIngresos" step="0.01" min="0" value="0" required>
                                                        <select class="form-select input-group-currency" id="impuestoIngresosMoneda">
                                                            <option value="USD">USD</option>
                                                            <option value="BS">Bs</option>
                                                        </select>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Alícuota (%)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="impuestoAlicuota" step="0.01" min="0" max="100" value="2.00" required>
                                                        <span class="input-group-text">%</span>
                                                    </div>
                                                    <small class="text-muted">Según ordenanza municipal</small>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Exoneraciones o Descuentos</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="impuestoExoneracion" step="0.01" min="0" max="100" value="0" required>
                                                        <span class="input-group-text">%</span>
                                                    </div>
                                                </div>
                                                
                                                <div class="formula-display">
                                                    <strong>Fórmula:</strong><br>
                                                    <span>Ingresos × (Alícuota / 100) × (1 - Exoneración / 100) = Impuesto Municipal</span>
                                                </div>
                                                
                                                <div class="d-grid">
                                                    <button class="btn btn-impuestos" onclick="calcularImpuestoMunicipal()">
                                                        <i class="fas fa-calculator me-2"></i>Calcular Impuesto Municipal
                                                    </button>
                                                </div>
                                                
                                                <div class="mt-4 p-3 border rounded bg-light">
                                                    <h6>Resultado del Cálculo:</h6>
                                                    <div class="row">
                                                        <div class="col-md-6">
                                                            <small>Base Imponible:</small>
                                                            <div class="metric-value" id="impuestoMunicipalBase">$0.00</div>
                                                        </div>
                                                        <div class="col-md-6">
                                                            <small>Impuesto a Pagar:</small>
                                                            <div class="metric-value" id="impuestoMunicipalPagar">$0.00</div>
                                                        </div>
                                                    </div>
                                                    <div class="mt-2">
                                                        <small>Ahorro por Exoneración:</small>
                                                        <div class="metric-value text-success" id="impuestoMunicipalAhorro">$0.00</div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Impuestos Municipales por Planta -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header impuestos">
                                                <i class="fas fa-industry me-2"></i>Impuestos Municipales por Planta
                                            </div>
                                            <div class="card-body">
                                                <div class="table-responsive">
                                                    <table class="table table-sm">
                                                        <thead>
                                                            <tr>
                                                                <th>Planta</th>
                                                                <th>Municipio</th>
                                                                <th>Alícuota %</th>
                                                                <th>Ingresos USD</th>
                                                                <th>Impuesto USD</th>
                                                                <th>Acción</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaImpuestosPlantas">
                                                            <tr>
                                                                <td>Planta Ocumare</td>
                                                                <td>Ocumare del Tuy</td>
                                                                <td>1.80%</td>
                                                                <td>$1,500,000</td>
                                                                <td>$27,000.00</td>
                                                                <td>
                                                                    <button class="btn btn-sm btn-outline-primary" onclick="editarImpuestoPlanta(0)">
                                                                        <i class="fas fa-edit"></i>
                                                                    </button>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>Cantera San Bernardo</td>
                                                                <td>Tomas Lander</td>
                                                                <td>2.00%</td>
                                                                <td>$500,000</td>
                                                                <td>$10,000.00</td>
                                                                <td>
                                                                    <button class="btn btn-sm btn-outline-primary" onclick="editarImpuestoPlanta(1)">
                                                                        <i class="fas fa-edit"></i>
                                                                    </button>
                                                                </td>
                                                            </tr>
                                                        </tbody>
                                                        <tfoot>
                                                            <tr class="total-row">
                                                                <td colspan="4" class="text-end"><strong>TOTAL:</strong></td>
                                                                <td><strong id="totalImpuestosPlantas">$37,000.00</strong></td>
                                                                <td></td>
                                                            </tr>
                                                        </tfoot>
                                                    </table>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <button class="btn btn-sm btn-impuestos" onclick="agregarImpuestoPlanta()">
                                                        <i class="fas fa-plus me-1"></i>Agregar Planta
                                                    </button>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Periodicidad de Pago</h6>
                                                    <div class="input-group mb-3">
                                                        <span class="input-group-text">Frecuencia</span>
                                                        <select class="form-select" id="frecuenciaImpuestosMunicipales">
                                                            <option value="mensual">Mensual</option>
                                                            <option value="trimestral">Trimestral</option>
                                                            <option value="semestral">Semestral</option>
                                                            <option value="anual">Anual</option>
                                                        </select>
                                                    </div>
                                                    <small class="text-muted">Los impuestos municipales se calculan según la frecuencia establecida</small>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Áreas -->
                            <div class="tab-pane fade" id="impuestos-areas">
                                <div class="row">
                                    <!-- Impuestos por Área Otorgada -->
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header impuestos">
                                                <i class="fas fa-map me-2"></i>Impuestos por Área Otorgada
                                            </div>
                                            <div class="card-body">
                                                <div class="table-responsive">
                                                    <table class="table table-hover">
                                                        <thead>
                                                            <tr>
                                                                <th>Cantera / Código SIG</th>
                                                                <th>Área Otorgada (Ha)</th>
                                                                <th>Múltiplo Entero</th>
                                                                <th>Cantidad x Hectárea (€)</th>
                                                                <th>Total Euros (€)</th>
                                                                <th>% Exoneración</th>
                                                                <th>Cantidad a Pagar (€)</th>
                                                                <th>Equivalente USD</th>
                                                                <th>Acción</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaAreasOtorgadas">
                                                            <tr>
                                                                <td>Cantera San Bernardo</td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="14.50" required>
                                                                </td>
                                                                <td>15</td>
                                                                <td>1,000.00</td>
                                                                <td>15,000.00</td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" max="100" value="70" required>
                                                                </td>
                                                                <td>4,500.00</td>
                                                                <td>$4,815.00</td>
                                                                <td>
                                                                    <button class="btn btn-sm btn-outline-primary">
                                                                        <i class="fas fa-eye preview-icon" onclick="previewPDFArea(0)"></i>
                                                                    </button>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>Cantera La Cabrera</td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="2.94" required>
                                                                </td>
                                                                <td>3</td>
                                                                <td>1,000.00</td>
                                                                <td>3,000.00</td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" max="100" value="70" required>
                                                                </td>
                                                                <td>900.00</td>
                                                                <td>$963.00</td>
                                                                <td>
                                                                    <button class="btn btn-sm btn-outline-primary">
                                                                        <i class="fas fa-eye preview-icon" onclick="previewPDFArea(1)"></i>
                                                                    </button>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>Cantera El Melero</td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="18.00" required>
                                                                </td>
                                                                <td>18</td>
                                                                <td>1,000.00</td>
                                                                <td>18,000.00</td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" max="100" value="70" required>
                                                                </td>
                                                                <td>5,400.00</td>
                                                                <td>$5,778.00</td>
                                                                <td>
                                                                    <button class="btn btn-sm btn-outline-primary">
                                                                        <i class="fas fa-eye preview-icon" onclick="previewPDFArea(2)"></i>
                                                                    </button>
                                                                </td>
                                                            </tr>
                                                            <tr>
                                                                <td>Cantera Mume</td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" value="7.10" required>
                                                                </td>
                                                                <td>8</td>
                                                                <td>1,000.00</td>
                                                                <td>8,000.00</td>
                                                                <td>
                                                                    <input type="number" class="form-control form-control-sm" step="0.01" min="0" max="100" value="70" required>
                                                                </td>
                                                                <td>2,400.00</td>
                                                                <td>$2,568.00</td>
                                                                <td>
                                                                    <button class="btn btn-sm btn-outline-primary">
                                                                        <i class="fas fa-eye preview-icon" onclick="previewPDFArea(3)"></i>
                                                                    </button>
                                                                </td>
                                                            </tr>
                                                        </tbody>
                                                        <tfoot>
                                                            <tr class="total-row">
                                                                <td><strong>TOTALES</strong></td>
                                                                <td><strong id="totalHectareas">42.54 Ha</strong></td>
                                                                <td><strong>44</strong></td>
                                                                <td></td>
                                                                <td><strong id="totalEuros">44,000.00 €</strong></td>
                                                                <td></td>
                                                                <td><strong id="totalPagarEuros">13,200.00 €</strong></td>
                                                                <td><strong id="totalPagarUsd">$14,124.00</strong></td>
                                                                <td></td>
                                                            </tr>
                                                        </tfoot>
                                                    </table>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-4">
                                                        <div class="mb-3">
                                                            <label class="form-label">Tasa de Cambio Euro a USD</label>
                                                            <div class="input-group">
                                                                <input type="number" class="form-control" id="tasaEuroUsd" step="0.0001" min="0" value="1.07" required>
                                                                <span class="input-group-text">USD/€</span>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="mb-3">
                                                            <label class="form-label">Valor x Hectárea (€)</label>
                                                            <div class="input-group">
                                                                <input type="number" class="form-control" id="valorHectarea" step="0.01" min="0" value="1000.00" required>
                                                                <span class="input-group-text">€/Ha</span>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="mb-3">
                                                            <label class="form-label">% Exoneración Predeterminado</label>
                                                            <div class="input-group">
                                                                <input type="number" class="form-control" id="exoneracionPredet" step="0.01" min="0" max="100" value="70" required>
                                                                <span class="input-group-text">%</span>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-6">
                                                        <div class="mb-3">
                                                            <label class="form-label">Mes de Pago Anual</label>
                                                            <select class="form-select" id="mesPagoAreasOtorgadas">
                                                                <option value="1">Enero</option>
                                                                <option value="2">Febrero</option>
                                                                <option value="3">Marzo</option>
                                                                <option value="4">Abril</option>
                                                                <option value="5">Mayo</option>
                                                                <option value="6">Junio</option>
                                                                <option value="7">Julio</option>
                                                                <option value="8">Agosto</option>
                                                                <option value="9">Septiembre</option>
                                                                <option value="10">Octubre</option>
                                                                <option value="11">Noviembre</option>
                                                                <option value="12">Diciembre</option>
                                                            </select>
                                                            <small class="text-muted">El impuesto por área otorgada es anual y se paga en este mes</small>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="mb-3">
                                                            <label class="form-label">Fecha Límite de Pago</label>
                                                            <input type="date" class="form-control" id="fechaLimiteAreasOtorgadas">
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="d-grid gap-2 d-md-flex justify-content-md-end">
                                                    <button class="btn btn-impuestos" onclick="calcularAreasOtorgadas()">
                                                        <i class="fas fa-calculator me-2"></i>Recalcular Todas las Áreas
                                                    </button>
                                                    <button class="btn btn-success" onclick="guardarImpuestos()">
                                                        <i class="fas fa-save me-2"></i>Guardar Impuestos
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Resumen -->
                            <div class="tab-pane fade" id="impuestos-resumen">
                                <div class="row">
                                    <!-- Resumen de Impuestos -->
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header impuestos">
                                                <i class="fas fa-chart-pie me-2"></i>Resumen General de Impuestos
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-3">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenTotalMineros">$0.00</div>
                                                            <div class="financial-label">Impuestos Mineros</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenTotalMunicipales">$0.00</div>
                                                            <div class="financial-label">Impuestos Municipales</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenTotalAreas">$0.00</div>
                                                            <div class="financial-label">Áreas Otorgadas</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="financial-metric bg-primary text-white">
                                                            <div class="financial-value" id="resumenTotalGeneralImpuestos">$0.00</div>
                                                            <div class="financial-label">Total Impuestos</div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Distribución de Impuestos</h6>
                                                    <div class="chart-container">
                                                        <canvas id="distribucionImpuestosChart"></canvas>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Detalle por Tipo de Impuesto</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Tipo</th>
                                                                    <th>Descripción</th>
                                                                    <th>Monto USD</th>
                                                                    <th>Monto Bs</th>
                                                                    <th>% del Total</th>
                                                                    <th>Estado</th>
                                                                    <th>Acción</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="detalleImpuestosResumen">
                                                                <tr>
                                                                    <td colspan="7" class="text-center">No hay datos</td>
                                                                </tr>
                                                            </tbody>
                                                        </table>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Consolidado Mensual</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Mes</th>
                                                                    <th>Mineros</th>
                                                                    <th>Municipales</th>
                                                                    <th>Áreas*</th>
                                                                    <th>Total</th>
                                                                    <th>Tasa BCV</th>
                                                                    <th>Estado</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="consolidadoMensualImpuestos">
                                                                <tr>
                                                                    <td colspan="7" class="text-center">No hay períodos cerrados</td>
                                                                </tr>
                                                            </tbody>
                                                            <tfoot>
                                                                <tr>
                                                                    <td colspan="7" class="text-muted"><small>*Áreas otorgadas se prorratean mensualmente</small></td>
                                                                </tr>
                                                            </tfoot>
                                                        </table>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Alertas -->
                            <div class="tab-pane fade" id="impuestos-alertas">
                                <div class="row">
                                    <!-- Alertas y Vencimientos -->
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header impuestos">
                                                <i class="fas fa-bell me-2"></i>Alertas de Vencimiento
                                            </div>
                                            <div class="card-body">
                                                <div class="alert alert-deadline">
                                                    <div class="row align-items-center">
                                                        <div class="col-md-8">
                                                            <h6><i class="fas fa-exclamation-triangle me-2"></i>Próximo Vencimiento</h6>
                                                            <p class="mb-0">Impuesto Minero - Caliza vence en <strong id="diasParaVencimiento">15 días</strong></p>
                                                            <small>Fecha límite: <span id="proximoVencimiento">--/--/----</span></small>
                                                        </div>
                                                        <div class="col-md-4 text-end">
                                                            <button class="btn btn-warning" onclick="generarReporteImpuestos()">
                                                                <i class="fas fa-file-pdf me-2"></i>Generar Reporte
                                                            </button>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="p-3 border rounded">
                                                            <small>Total Impuestos Mineros</small>
                                                            <div class="metric-value" id="totalImpuestosMineros">$0.00</div>
                                                            <div class="metric-unit" id="estadoMineros">Sin vencimientos</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="p-3 border rounded">
                                                            <small>Total Impuestos Municipales</small>
                                                            <div class="metric-value" id="totalImpuestosMunicipales">$0.00</div>
                                                            <div class="metric-unit" id="estadoMunicipales">Al día</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="p-3 border rounded">
                                                            <small>Total Áreas Otorgadas</small>
                                                            <div class="metric-value" id="totalAreasOtorgadas">$0.00</div>
                                                            <div class="metric-unit" id="estadoAreas">Próximo pago: --/--</div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Calendario de Vencimientos</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Impuesto</th>
                                                                    <th>Descripción</th>
                                                                    <th>Fecha Límite</th>
                                                                    <th>Días Restantes</th>
                                                                    <th>Monto USD</th>
                                                                    <th>Estado</th>
                                                                    <th>Acción</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="calendarioVencimientos">
                                                                <tr>
                                                                    <td colspan="7" class="text-center">No hay vencimientos configurados</td>
                                                                </tr>
                                                            </tbody>
                                                        </table>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3 text-center">
                                                    <div class="p-3 border rounded bg-light">
                                                        <h5>Total General de Impuestos</h5>
                                                        <div class="metric-value fs-3" id="totalGeneralImpuestos">$0.00</div>
                                                        <small class="text-muted">Equivalente en Bs: <span id="totalImpuestosBs">0.00 Bs</span></small>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Reportes -->
                    <div class="tab-pane fade" id="reportes" role="tabpanel">
                        <!-- Submenú de Reportes -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#reportes-resumen">Resumen Ejecutivo</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#reportes-detalle">Detalle por Provisión</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#reportes-exportacion">Exportación</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#reportes-visualizacion">Visualización</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#reportes-periodos">Períodos</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Resumen Ejecutivo -->
                            <div class="tab-pane fade show active" id="reportes-resumen">
                                <div class="periodo-selector">
                                    <div class="row align-items-center">
                                        <div class="col-md-6">
                                            <h5 class="mb-0">Resumen Ejecutivo</h5>
                                            <p class="mb-0 text-muted">Información consolidada del período actual</p>
                                        </div>
                                        <div class="col-md-6 text-end">
                                            <div class="input-group">
                                                <select class="form-select" id="selectPeriodoReporte">
                                                    <option value="actual">Período Actual</option>
                                                    <!-- Se llenará dinámicamente con períodos anteriores -->
                                                </select>
                                                <button class="btn btn-reportes" onclick="generarResumenEjecutivo()">
                                                    <i class="fas fa-sync-alt me-2"></i>Actualizar
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header reportes">
                                                <i class="fas fa-chart-line me-2"></i>Resumen Ejecutivo - VENCEMENT C.A.
                                            </div>
                                            <div class="card-body">
                                                <div class="metadata-display">
                                                    <div class="metadata-item">
                                                        <div class="metadata-label">Período:</div>
                                                        <div class="metadata-value" id="metadataPeriodo">--/----</div>
                                                    </div>
                                                    <div class="metadata-item">
                                                        <div class="metadata-label">Tasa BCV:</div>
                                                        <div class="metadata-value" id="metadataTasaBCV">0.00 Bs/$</div>
                                                    </div>
                                                    <div class="metadata-item">
                                                        <div class="metadata-label">Responsable:</div>
                                                        <div class="metadata-value" id="metadataResponsable">No asignado</div>
                                                    </div>
                                                    <div class="metadata-item">
                                                        <div class="metadata-label">Estado:</div>
                                                        <div class="metadata-value"><span id="metadataEstado" class="periodo-abierto badge">Abierto</span></div>
                                                    </div>
                                                    <div class="metadata-item">
                                                        <div class="metadata-label">Versión Sistema:</div>
                                                        <div class="metadata-value">4.0</div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-4">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenTotalProvisions">$0.00</div>
                                                            <div class="financial-label">Total Provisiones</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenTotalServices">$0.00</div>
                                                            <div class="financial-label">Total Servicios</div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="financial-metric">
                                                            <div class="financial-value" id="resumenTotalTaxes">$0.00</div>
                                                            <div class="financial-label">Total Impuestos</div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-3">
                                                        <div class="unit-cost-card">
                                                            <h6>Costo por Saco</h6>
                                                            <div class="unit-cost-value" id="costoPorSaco">$0.00</div>
                                                            <small class="text-muted">USD/saco (42.5kg)</small>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="unit-cost-card">
                                                            <h6>Costo por Tonelada</h6>
                                                            <div class="unit-cost-value" id="costoPorTonelada">$0.00</div>
                                                            <small class="text-muted">USD/ton cemento</small>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="unit-cost-card">
                                                            <h6>Costo Granel</h6>
                                                            <div class="unit-cost-value" id="costoGranel">$0.00</div>
                                                            <small class="text-muted">USD/ton granel</small>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="unit-cost-card">
                                                            <h6>Costo Total</h6>
                                                            <div class="unit-cost-value" id="costoTotalResumen">$0.00</div>
                                                            <small class="text-muted">USD total período</small>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Participación Porcentual por Insumo</h6>
                                                    <div class="table-responsive">
                                                        <table class="table table-sm">
                                                            <thead>
                                                                <tr>
                                                                    <th>Insumo</th>
                                                                    <th>Costo USD</th>
                                                                    <th>% del Total</th>
                                                                    <th>Tendencia</th>
                                                                </tr>
                                                            </thead>
                                                            <tbody id="participacionInsumos">
                                                                <tr>
                                                                    <td colspan="4" class="text-center">No hay datos</td>
                                                                </tr>
                                                            </tbody>
                                                        </table>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Indicadores de Eficiencia Clave</h6>
                                                    <div class="row">
                                                        <div class="col-md-4">
                                                            <div class="efficiency-indicator">
                                                                <div class="efficiency-label">kWh/ton Clinker</div>
                                                                <div class="efficiency-value" id="indicadorKwhClinker">0.00</div>
                                                                <small class="text-muted">Consumo eléctrico</small>
                                                            </div>
                                                        </div>
                                                        <div class="col-md-4">
                                                            <div class="efficiency-indicator">
                                                                <div class="efficiency-label">Nm³/ton Cemento</div>
                                                                <div class="efficiency-value" id="indicadorGasCemento">0.00</div>
                                                                <small class="text-muted">Consumo gas natural</small>
                                                            </div>
                                                        </div>
                                                        <div class="col-md-4">
                                                            <div class="efficiency-indicator">
                                                                <div class="efficiency-label">L gasoil/ton Acarreo</div>
                                                                <div class="efficiency-value" id="indicadorGasoilAcarreo">0.00</div>
                                                                <small class="text-muted">Eficiencia en acarreo</small>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4 text-center">
                                                    <div class="export-buttons">
                                                        <button class="btn btn-success" onclick="exportarResumenExcel()">
                                                            <i class="fas fa-file-excel me-2"></i>Exportar a Excel
                                                        </button>
                                                        <button class="btn btn-danger" onclick="exportarResumenPDF()">
                                                            <i class="fas fa-file-pdf me-2"></i>Exportar a PDF
                                                        </button>
                                                        <button class="btn btn-info" onclick="previewResumenPDF()">
                                                            <i class="fas fa-eye me-2"></i>Vista Previa PDF
                                                        </button>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Detalle por Provisión -->
                            <div class="tab-pane fade" id="reportes-detalle">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header reportes">
                                                <i class="fas fa-list-alt me-2"></i>Reporte Detallado por Provisión/Servicio
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-4">
                                                        <div class="search-box">
                                                            <i class="fas fa-search search-icon"></i>
                                                            <input type="text" id="searchProvisions" class="form-control" placeholder="Buscar provisiones...">
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <select class="form-select" id="filterCategory">
                                                            <option value="">Todas las categorías</option>
                                                            <option value="Energía">Energía</option>
                                                            <option value="Materias Primas">Materias Primas</option>
                                                            <option value="Servicios">Servicios</option>
                                                            <option value="Impuestos">Impuestos</option>
                                                            <option value="Almacén">Almacén</option>
                                                            <option value="Depreciación">Depreciación</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <select class="form-select" id="filterPeriodoDetalle">
                                                            <option value="actual">Período Actual</option>
                                                            <!-- Se llenará dinámicamente -->
                                                        </select>
                                                    </div>
                                                </div>
                                                
                                                <div class="table-responsive">
                                                    <table class="table data-table">
                                                        <thead>
                                                            <tr>
                                                                <th>Categoría</th>
                                                                <th>Descripción</th>
                                                                <th>Cantidad</th>
                                                                <th>Precio Unitario USD</th>
                                                                <th>Precio Unitario Bs</th>
                                                                <th>Monto USD</th>
                                                                <th>Monto Bs</th>
                                                                <th>Tasa BCV usada</th>
                                                                <th>Acción</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaDetalleProvisions">
                                                            <tr>
                                                                <td colspan="9" class="text-center">No hay datos disponibles</td>
                                                            </tr>
                                                        </tbody>
                                                        <tfoot>
                                                            <tr class="total-row">
                                                                <td colspan="5" class="text-end"><strong>TOTALES:</strong></td>
                                                                <td><strong id="totalDetalleUSD">$0.00</strong></td>
                                                                <td><strong id="totalDetalleBS">0.00 Bs</strong></td>
                                                                <td></td>
                                                                <td></td>
                                                            </tr>
                                                        </tfoot>
                                                    </table>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <div class="export-buttons">
                                                        <button class="btn btn-success" onclick="exportarDetalleExcel()">
                                                            <i class="fas fa-file-excel me-2"></i>Exportar Detalle a Excel
                                                        </button>
                                                        <button class="btn btn-danger" onclick="exportarDetallePDF()">
                                                            <i class="fas fa-file-pdf me-2"></i>Exportar Detalle a PDF
                                                        </button>
                                                        <button class="btn btn-info" onclick="generarReporteAuditoria()">
                                                            <i class="fas fa-clipboard-check me-2"></i>Reporte de Auditoría
                                                        </button>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4">
                                                    <h6>Logs de Cambios</h6>
                                                    <div class="audit-trail" id="auditTrail">
                                                        <div class="log-entry created">
                                                            <strong>Sistema iniciado</strong> - <small>Hoy 10:30 AM</small><br>
                                                            <span>Período actual abierto automáticamente</span>
                                                        </div>
                                                        <!-- Se llenará dinámicamente -->
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Exportación -->
                            <div class="tab-pane fade" id="reportes-exportacion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header reportes">
                                                <i class="fas fa-download me-2"></i>Exportación y Auditoría
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h5><i class="fas fa-file-excel text-success me-2"></i>Exportación a Excel</h5>
                                                                <p class="text-muted">Exporte datos en formato Excel listo para análisis.</p>
                                                                
                                                                <div class="mt-3">
                                                                    <label class="form-label">Seleccionar Período</label>
                                                                    <select class="form-select" id="selectPeriodoExcel">
                                                                        <option value="actual">Período Actual</option>
                                                                    </select>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <label class="form-label">Seleccionar Módulos</label>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkProduccionExcel" checked>
                                                                        <label class="form-check-label" for="checkProduccionExcel">Producción</label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkServiciosExcel" checked>
                                                                        <label class="form-check-label" for="checkServiciosExcel">Servicios</label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkImpuestosExcel" checked>
                                                                        <label class="form-check-label" for="checkImpuestosExcel">Impuestos</label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkAlmacenExcel">
                                                                        <label class="form-check-label" for="checkAlmacenExcel">Almacén</label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkActivosExcel">
                                                                        <label class="form-check-label" for="checkActivosExcel">Activos Fijos</label>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <button class="btn btn-success w-100" onclick="exportarExcelCompleto()">
                                                                        <i class="fas fa-file-excel me-2"></i>Exportar a Excel
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h5><i class="fas fa-file-pdf text-danger me-2"></i>Exportación a PDF</h5>
                                                                <p class="text-muted">Genere reportes PDF audit-ready con metadatos.</p>
                                                                
                                                                <div class="mt-3">
                                                                    <label class="form-label">Seleccionar Período</label>
                                                                    <select class="form-select" id="selectPeriodoPDF">
                                                                        <option value="actual">Período Actual</option>
                                                                    </select>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <label class="form-label">Tipo de Reporte</label>
                                                                    <select class="form-select" id="selectTipoReportePDF">
                                                                        <option value="resumen">Resumen Ejecutivo</option>
                                                                        <option value="detalle">Detalle Completo</option>
                                                                        <option value="auditoria">Reporte de Auditoría</option>
                                                                        <option value="consolidado">Consolidado Mensual</option>
                                                                    </select>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkFirmaDigital" checked>
                                                                        <label class="form-check-label" for="checkFirmaDigital">Incluir firma digital</label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkMetadatos" checked>
                                                                        <label class="form-check-label" for="checkMetadatos">Incluir metadatos</label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkLogsCambios">
                                                                        <label class="form-check-label" for="checkLogsCambios">Incluir logs de cambios</label>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <button class="btn btn-danger w-100" onclick="exportarPDFCompleto()">
                                                                        <i class="fas fa-file-pdf me-2"></i>Exportar a PDF
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h5><i class="fas fa-clipboard-list text-primary me-2"></i>Metadatos del Reporte</h5>
                                                                <div class="metadata-display">
                                                                    <div class="metadata-item">
                                                                        <div class="metadata-label">Período Reporte:</div>
                                                                        <div class="metadata-value" id="metaPeriodoReporte">--/----</div>
                                                                    </div>
                                                                    <div class="metadata-item">
                                                                        <div class="metadata-label">Tasa BCV:</div>
                                                                        <div class="metadata-value" id="metaTasaBCVReporte">0.00 Bs/$</div>
                                                                    </div>
                                                                    <div class="metadata-item">
                                                                        <div class="metadata-label">Responsable:</div>
                                                                        <div class="metadata-value" id="metaResponsableReporte">No asignado</div>
                                                                    </div>
                                                                    <div class="metadata-item">
                                                                        <div class="metadata-label">Fecha Generación:</div>
                                                                        <div class="metadata-value" id="metaFechaGeneracion">--/--/---- --:--</div>
                                                                    </div>
                                                                    <div class="metadata-item">
                                                                        <div class="metadata-label">Versión Sistema:</div>
                                                                        <div class="metadata-value">4.0</div>
                                                                    </div>
                                                                    <div class="metadata-item">
                                                                        <div class="metadata-label">Hash/Firma:</div>
                                                                        <div class="metadata-value">
                                                                            <div class="digital-signature" id="metaHashReporte">
                                                                                Generar reporte para ver firma digital
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h5><i class="fas fa-history text-warning me-2"></i>Logs de Auditoría</h5>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Fecha/Hora</th>
                                                                                <th>Usuario</th>
                                                                                <th>Acción</th>
                                                                                <th>Módulo</th>
                                                                                <th>Detalle</th>
                                                                                <th>Impacto</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaLogsAuditoria">
                                                                            <tr>
                                                                                <td>--/--/---- --:--</td>
                                                                                <td>Sistema</td>
                                                                                <td>Inicio</td>
                                                                                <td>Sistema</td>
                                                                                <td>Sistema iniciado</td>
                                                                                <td>-</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                                
                                                                <div class="mt-3 text-center">
                                                                    <button class="btn btn-warning" onclick="exportarLogsAuditoria()">
                                                                        <i class="fas fa-download me-2"></i>Exportar Logs de Auditoría
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Visualización -->
                            <div class="tab-pane fade" id="reportes-visualizacion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header reportes">
                                                <i class="fas fa-chart-bar me-2"></i>Visualización Gráfica
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-4">
                                                        <select class="form-select" id="selectPeriodoGrafico">
                                                            <option value="actual">Período Actual</option>
                                                            <option value="comparativo">Comparativo 3 meses</option>
                                                            <option value="anual">Evolución Anual</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <select class="form-select" id="selectTipoGrafico">
                                                            <option value="barras">Barras - Costos por Categoría</option>
                                                            <option value="torta">Torta - Participación Porcentual</option>
                                                            <option value="linea">Línea - Evolución Temporal</option>
                                                            <option value="comparativo">Comparativo Multi-planta</option>
                                                            <option value="heatmap">Heatmap por Rubro</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <button class="btn btn-reportes w-100" onclick="generarVisualizaciones()">
                                                            <i class="fas fa-chart-bar me-2"></i>Generar Visualizaciones
                                                        </button>
                                                    </div>
                                                </div>
                                                
                                                <div class="visualization-grid">
                                                    <div class="visualization-card">
                                                        <div class="visualization-title" id="tituloGrafico1">Costos por Categoría</div>
                                                        <div class="chart-container">
                                                            <canvas id="graficoBarrasCategorias"></canvas>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="visualization-card">
                                                        <div class="visualization-title" id="tituloGrafico2">Participación Porcentual</div>
                                                        <div class="chart-container">
                                                            <canvas id="graficoTortaParticipacion"></canvas>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="visualization-card">
                                                        <div class="visualization-title" id="tituloGrafico3">Evolución Temporal</div>
                                                        <div class="timeline-container">
                                                            <canvas id="graficoLineaEvolucion"></canvas>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="visualization-card">
                                                        <div class="visualization-title" id="tituloGrafico4">Comparativo Multi-planta</div>
                                                        <div class="comparative-chart">
                                                            <canvas id="graficoComparativoPlantas"></canvas>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h5><i class="fas fa-fire me-2"></i>Heatmap por Rubro</h5>
                                                                <div id="heatmapRubros" class="heatmap-container">
                                                                    <div class="text-center p-4">
                                                                        <i class="fas fa-chart-bar fa-2x text-muted"></i>
                                                                        <p class="mt-2">Seleccione "Heatmap por Rubro" y genere visualizaciones</p>
                                                                    </div>
                                                                </div>
                                                                <div class="color-scale mt-3" id="escalaColoresHeatmap" style="display: none;">
                                                                    <div class="color-scale-item">
                                                                        <div class="color-box" style="background-color: #d6eaf8;"></div>
                                                                        <span>Bajo</span>
                                                                    </div>
                                                                    <div class="color-scale-item">
                                                                        <div class="color-box" style="background-color: #85c1e9;"></div>
                                                                        <span>Medio</span>
                                                                    </div>
                                                                    <div class="color-scale-item">
                                                                        <div class="color-box" style="background-color: #2e86c1;"></div>
                                                                        <span>Alto</span>
                                                                    </div>
                                                                    <div class="color-scale-item">
                                                                        <div class="color-box" style="background-color: #1b4f72;"></div>
                                                                        <span>Muy Alto</span>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-4 text-center">
                                                    <div class="export-buttons justify-content-center">
                                                        <button class="btn btn-success" onclick="exportarGraficosExcel()">
                                                            <i class="fas fa-file-excel me-2"></i>Exportar Datos Gráficos
                                                        </button>
                                                        <button class="btn btn-danger" onclick="exportarGraficosPDF()">
                                                            <i class="fas fa-file-pdf me-2"></i>Exportar Gráficos a PDF
                                                        </button>
                                                        <button class="btn btn-info" onclick="guardarConfiguracionGraficos()">
                                                            <i class="fas fa-save me-2"></i>Guardar Configuración
                                                        </button>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Períodos -->
                            <div class="tab-pane fade" id="reportes-periodos">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header reportes">
                                                <i class="fas fa-calendar-alt me-2"></i>Gestión de Períodos Contables
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-4">
                                                    <div class="col-md-8">
                                                        <h5>Período Actual</h5>
                                                        <div class="p-3 border rounded bg-light">
                                                            <div class="row">
                                                                <div class="col-md-4">
                                                                    <strong>Mes/Año:</strong><br>
                                                                    <span id="periodoActualNombre">--/----</span>
                                                                </div>
                                                                <div class="col-md-4">
                                                                    <strong>Estado:</strong><br>
                                                                    <span id="periodoActualEstado" class="periodo-abierto badge">Abierto</span>
                                                                </div>
                                                                <div class="col-md-4">
                                                                    <strong>Responsable:</strong><br>
                                                                    <span id="periodoActualResponsable">No asignado</span>
                                                                </div>
                                                            </div>
                                                            <div class="row mt-2">
                                                                <div class="col-md-12">
                                                                    <strong>Tasa BCV:</strong>
                                                                    <span id="periodoActualTasaBCV">0.00 Bs/$</span>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="d-grid gap-2">
                                                            <button class="btn btn-success" id="btnAperturarPeriodo" onclick="aperturarPeriodo()">
                                                                <i class="fas fa-folder-open me-2"></i>Aperturar Período
                                                            </button>
                                                            <button class="btn btn-danger" id="btnCerrarPeriodo" onclick="cerrarPeriodo()" disabled>
                                                                <i class="fas fa-lock me-2"></i>Cerrar Período
                                                            </button>
                                                            <button class="btn btn-warning" onclick="mostrarModalCorreccion()">
                                                                <i class="fas fa-edit me-2"></i>Nota de Corrección
                                                            </button>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row">
                                                    <div class="col-md-12">
                                                        <h5>Períodos Anteriores</h5>
                                                        <div class="row mb-3">
                                                            <div class="col-md-3">
                                                                <select class="form-select" id="filterAnioPeriodos">
                                                                    <option value="">Todos los años</option>
                                                                    <option value="2024">2024</option>
                                                                    <option value="2025">2025</option>
                                                                    <option value="2026" selected>2026</option>
                                                                </select>
                                                            </div>
                                                            <div class="col-md-3">
                                                                <select class="form-select" id="filterEstadoPeriodos">
                                                                    <option value="">Todos los estados</option>
                                                                    <option value="abierto">Abierto</option>
                                                                    <option value="cerrado">Cerrado</option>
                                                                </select>
                                                            </div>
                                                            <div class="col-md-6 text-end">
                                                                <button class="btn btn-info" onclick="cargarPeriodosAnteriores()">
                                                                    <i class="fas fa-sync-alt me-2"></i>Actualizar Lista
                                                                </button>
                                                            </div>
                                                        </div>
                                                        
                                                        <div class="table-responsive">
                                                            <table class="table table-hover">
                                                                <thead>
                                                                    <tr>
                                                                        <th>Período</th>
                                                                        <th>Tasa BCV</th>
                                                                        <th>Provisiones</th>
                                                                        <th>Servicios</th>
                                                                        <th>Producción</th>
                                                                        <th>Impuestos</th>
                                                                        <th>Total</th>
                                                                        <th>Estado</th>
                                                                        <th>Acciones</th>
                                                                    </tr>
                                                                </thead>
                                                                <tbody id="tablaPeriodosAnteriores">
                                                                    <tr>
                                                                        <td colspan="9" class="text-center">No hay períodos anteriores</td>
                                                                    </tr>
                                                                </tbody>
                                                            </table>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h5><i class="fas fa-chart-line me-2"></i>Comparativo de Períodos</h5>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoComparativoPeriodos"></canvas>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <div class="row">
                                                                        <div class="col-md-4">
                                                                            <div class="form-check">
                                                                                <input class="form-check-input" type="checkbox" id="checkCompararProvisiones" checked>
                                                                                <label class="form-check-label" for="checkCompararProvisiones">Provisiones</label>
                                                                            </div>
                                                                        </div>
                                                                        <div class="col-md-4">
                                                                            <div class="form-check">
                                                                                <input class="form-check-input" type="checkbox" id="checkCompararServicios" checked>
                                                                                <label class="form-check-label" for="checkCompararServicios">Servicios</label>
                                                                            </div>
                                                                        </div>
                                                                        <div class="col-md-4">
                                                                            <div class="form-check">
                                                                                <input class="form-check-input" type="checkbox" id="checkCompararImpuestos" checked>
                                                                                <label class="form-check-label" for="checkCompararImpuestos">Impuestos</label>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mt-3 text-center">
                                                                    <button class="btn btn-reportes" onclick="generarComparativoPeriodos()">
                                                                        <i class="fas fa-balance-scale me-2"></i>Generar Comparativo
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Almacén -->
                    <div class="tab-pane fade" id="almacen" role="tabpanel">
                        <!-- Submenú de Almacén -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#almacen-clasificacion">Clasificación</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#almacen-movimientos">Movimientos</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#almacen-costeo">Costeo</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#almacen-reportes">Reportes</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#almacen-alertas">Alertas</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Clasificación -->
                            <div class="tab-pane fade show active" id="almacen-clasificacion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header almacen">
                                                <i class="fas fa-boxes me-2"></i>Clasificación de Insumos
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-6">
                                                        <button class="btn btn-almacen" onclick="mostrarModalNuevoInsumo()">
                                                            <i class="fas fa-plus me-2"></i>Nuevo Insumo
                                                        </button>
                                                        <button class="btn btn-outline-secondary ms-2" onclick="exportarCatalogoInsumos()">
                                                            <i class="fas fa-download me-2"></i>Exportar Catálogo
                                                        </button>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="search-box">
                                                            <i class="fas fa-search search-icon"></i>
                                                            <input type="text" id="searchInsumos" class="form-control" placeholder="Buscar insumos...">
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="table-responsive">
                                                    <table class="table table-hover">
                                                        <thead>
                                                            <tr>
                                                                <th>Código</th>
                                                                <th>Descripción</th>
                                                                <th>Categoría</th>
                                                                <th>Unidad</th>
                                                                <th>Stock Inicial</th>
                                                                <th>Stock Actual</th>
                                                                <th>Valor Unitario USD</th>
                                                                <th>Acciones</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaInsumos">
                                                            <tr>
                                                                <td colspan="8" class="text-center">No hay insumos registrados</td>
                                                            </tr>
                                                        </tbody>
                                                    </table>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Materias Primas</h6>
                                                                <div class="metric-value" id="totalMateriasPrimas">0</div>
                                                                <div class="metric-unit">Insumos registrados</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Repuestos</h6>
                                                                <div class="metric-value" id="totalRepuestos">0</div>
                                                                <div class="metric-unit">Insumos registrados</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Consumibles</h6>
                                                                <div class="metric-value" id="totalConsumibles">0</div>
                                                                <div class="metric-unit">Insumos registrados</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Movimientos -->
                            <div class="tab-pane fade" id="almacen-movimientos">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header almacen">
                                                <i class="fas fa-exchange-alt me-2"></i>Registro de Movimientos
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-3">
                                                        <select class="form-select" id="filterTipoMovimiento">
                                                            <option value="">Todos los tipos</option>
                                                            <option value="entrada">Entradas</option>
                                                            <option value="salida">Salidas</option>
                                                            <option value="ajuste">Ajustes</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <select class="form-select" id="filterInsumoMovimiento">
                                                            <option value="">Todos los insumos</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <input type="date" class="form-control" id="filterFechaDesde">
                                                    </div>
                                                    <div class="col-md-3">
                                                        <input type="date" class="form-control" id="filterFechaHasta">
                                                    </div>
                                                </div>
                                                
                                                <div class="row mb-3">
                                                    <div class="col-md-12 text-end">
                                                        <button class="btn btn-almacen" onclick="mostrarModalNuevoMovimiento()">
                                                            <i class="fas fa-plus me-2"></i>Nuevo Movimiento
                                                        </button>
                                                    </div>
                                                </div>
                                                
                                                <div class="table-responsive">
                                                    <table class="table table-hover kardex-table">
                                                        <thead>
                                                            <tr>
                                                                <th>Fecha</th>
                                                                <th>Tipo</th>
                                                                <th>Insumo</th>
                                                                <th>Cantidad</th>
                                                                <th>Costo Unitario USD</th>
                                                                <th>Costo Unitario Bs</th>
                                                                <th>Tasa BCV</th>
                                                                <th>Responsable</th>
                                                                <th>Acciones</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaMovimientos">
                                                            <tr>
                                                                <td colspan="9" class="text-center">No hay movimientos registrados</td>
                                                            </tr>
                                                        </tbody>
                                                    </table>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Total Entradas</h6>
                                                                <div class="metric-value" id="totalEntradasAlmacen">0</div>
                                                                <div class="metric-unit">Unidades</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Total Salidas</h6>
                                                                <div class="metric-value" id="totalSalidasAlmacen">0</div>
                                                                <div class="metric-unit">Unidades</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Valor Stock Actual</h6>
                                                                <div class="metric-value" id="valorStockActual">$0.00</div>
                                                                <div class="metric-unit">USD</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Costeo -->
                            <div class="tab-pane fade" id="almacen-costeo">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header almacen">
                                                <i class="fas fa-calculator me-2"></i>Costeo Automático
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Método de Valoración</h6>
                                                                <select class="form-select" id="selectMetodoValoracion">
                                                                    <option value="fifo">FIFO (Primero en Entrar, Primero en Salir)</option>
                                                                    <option value="promedio" selected>Promedio Ponderado</option>
                                                                    <option value="costo-especifico">Costo Específico</option>
                                                                </select>
                                                                <small class="text-muted">Este método afecta el cálculo del costo de salidas</small>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-8">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Conversión Automática</h6>
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <label class="form-label">Monto en USD</label>
                                                                        <div class="input-group">
                                                                            <input type="number" class="form-control" id="montoUSD" value="1000" step="0.01">
                                                                            <span class="input-group-text">USD</span>
                                                                        </div>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <label class="form-label">Equivalente en Bs</label>
                                                                        <div class="input-group">
                                                                            <input type="number" class="form-control" id="montoBS" value="36000" step="0.01" readonly>
                                                                            <span class="input-group-text">Bs</span>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="row mt-2">
                                                                    <div class="col-md-12">
                                                                        <label class="form-label">Tasa BCV</label>
                                                                        <div class="input-group">
                                                                            <input type="number" class="form-control" id="tasaConversion" value="36.00" step="0.0001">
                                                                            <span class="input-group-text">Bs/$</span>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="mt-2">
                                                                    <button class="btn btn-sm btn-almacen" onclick="calcularConversion()">
                                                                        <i class="fas fa-sync-alt me-1"></i>Calcular Conversión
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Kardex por Ítem</h6>
                                                                <div class="row mb-3">
                                                                    <div class="col-md-6">
                                                                        <select class="form-select" id="selectInsumoKardex">
                                                                            <option value="">Seleccionar insumo...</option>
                                                                        </select>
                                                                    </div>
                                                                    <div class="col-md-6 text-end">
                                                                        <button class="btn btn-almacen" onclick="generarKardex()">
                                                                            <i class="fas fa-file-alt me-2"></i>Generar Kardex
                                                                        </button>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm kardex-table">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Fecha</th>
                                                                                <th>Movimiento</th>
                                                                                <th>Entrada</th>
                                                                                <th>Salida</th>
                                                                                <th>Saldo</th>
                                                                                <th>Costo Unitario USD</th>
                                                                                <th>Costo Total USD</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaKardex">
                                                                            <tr>
                                                                                <td colspan="7" class="text-center">Seleccione un insumo para ver el kardex</td>
                                                                            </tr>
                                                                        </tbody>
                                                                        <tfoot id="footerKardex" style="display: none;">
                                                                            <tr class="total-row">
                                                                                <td colspan="2"><strong>RESUMEN</strong></td>
                                                                                <td><strong id="totalEntradasKardex">0</strong></td>
                                                                                <td><strong id="totalSalidasKardex">0</strong></td>
                                                                                <td><strong id="saldoFinalKardex">0</strong></td>
                                                                                <td><strong id="costoPromedioKardex">$0.00</strong></td>
                                                                                <td><strong id="valorStockKardex">$0.00</strong></td>
                                                                            </tr>
                                                                        </tfoot>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Reportes -->
                            <div class="tab-pane fade" id="almacen-reportes">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header almacen">
                                                <i class="fas fa-chart-pie me-2"></i>Reportes de Almacén
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Consumo Mensual</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoConsumoMensual"></canvas>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-8">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Participación en el Costo Total</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoParticipacionAlmacen"></canvas>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Integración con Otros Módulos</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Módulo</th>
                                                                                <th>Salidas Relacionadas</th>
                                                                                <th>Valor Total USD</th>
                                                                                <th>% del Total Almacén</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaIntegracionAlmacen">
                                                                            <tr>
                                                                                <td>Producción</td>
                                                                                <td>0</td>
                                                                                <td>$0.00</td>
                                                                                <td>0%</td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Servicios</td>
                                                                                <td>0</td>
                                                                                <td>$0.00</td>
                                                                                <td>0%</td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Mantenimiento</td>
                                                                                <td>0</td>
                                                                                <td>$0.00</td>
                                                                                <td>0%</td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Comedor</td>
                                                                                <td>0</td>
                                                                                <td>$0.00</td>
                                                                                <td>0%</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Exportación de Reportes</h6>
                                                                <div class="export-buttons">
                                                                    <button class="btn btn-success" onclick="exportarReporteAlmacenExcel()">
                                                                        <i class="fas fa-file-excel me-2"></i>Reporte Excel
                                                                    </button>
                                                                    <button class="btn btn-danger" onclick="exportarReporteAlmacenPDF()">
                                                                        <i class="fas fa-file-pdf me-2"></i>Reporte PDF
                                                                    </button>
                                                                    <button class="btn btn-info" onclick="exportarKardexCompleto()">
                                                                        <i class="fas fa-list-alt me-2"></i>Kardex Completo
                                                                    </button>
                                                                    <button class="btn btn-warning" onclick="exportarMovimientosAlmacen()">
                                                                        <i class="fas fa-exchange-alt me-2"></i>Movimientos
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Alertas -->
                            <div class="tab-pane fade" id="almacen-alertas">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header almacen">
                                                <i class="fas fa-bell me-2"></i>Alertas de Stock
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-12">
                                                        <button class="btn btn-almacen" onclick="mostrarModalConfigurarAlertas()">
                                                            <i class="fas fa-cog me-2"></i>Configurar Alertas
                                                        </button>
                                                    </div>
                                                </div>
                                                
                                                <div id="alertasStockContainer">
                                                    <div class="alert alert-warning">
                                                        <i class="fas fa-exclamation-triangle me-2"></i>
                                                        No hay alertas de stock configuradas
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Ítems con Stock Bajo</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Insumo</th>
                                                                                <th>Stock Actual</th>
                                                                                <th>Stock Mínimo</th>
                                                                                <th>Diferencia</th>
                                                                                <th>Estado</th>
                                                                                <th>Acción</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaStockBajo">
                                                                            <tr>
                                                                                <td colspan="6" class="text-center">No hay ítems con stock bajo</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-6">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Configuración de Alertas</h6>
                                                                <div class="form-check">
                                                                    <input class="form-check-input" type="checkbox" id="checkAlertasEmail" checked>
                                                                    <label class="form-check-label" for="checkAlertasEmail">
                                                                        Enviar alertas por email
                                                                    </label>
                                                                </div>
                                                                <div class="form-check">
                                                                    <input class="form-check-input" type="checkbox" id="checkAlertasNotificacion" checked>
                                                                    <label class="form-check-label" for="checkAlertasNotificacion">
                                                                        Mostrar notificaciones en sistema
                                                                    </label>
                                                                </div>
                                                                <div class="form-check">
                                                                    <input class="form-check-input" type="checkbox" id="checkAlertasReporte">
                                                                    <label class="form-check-label" for="checkAlertasReporte">
                                                                        Generar reporte semanal
                                                                    </label>
                                                                </div>
                                                                <div class="mt-3">
                                                                    <label class="form-label">Días para alerta temprana</label>
                                                                    <input type="number" class="form-control" id="diasAlertaTemprana" value="7" min="1" max="30">
                                                                </div>
                                                                <div class="mt-3">
                                                                    <button class="btn btn-almacen w-100" onclick="guardarConfiguracionAlertas()">
                                                                        <i class="fas fa-save me-2"></i>Guardar Configuración
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Estadísticas de Alertas</h6>
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <div class="metric-value" id="totalAlertasMes">0</div>
                                                                        <div class="metric-unit">Alertas este mes</div>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <div class="metric-value" id="itemsStockBajo">0</div>
                                                                        <div class="metric-unit">Ítems con stock bajo</div>
                                                                    </div>
                                                                </div>
                                                                <div class="row mt-3">
                                                                    <div class="col-md-6">
                                                                        <div class="metric-value" id="tiempoRespuesta">0 h</div>
                                                                        <div class="metric-unit">Tiempo promedio respuesta</div>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <div class="metric-value" id="eficienciaReposicion">0%</div>
                                                                        <div class="metric-unit">Eficiencia en reposición</div>
                                                                    </div>
                                                                </div>
                                                                <div class="mt-3">
                                                                    <button class="btn btn-info w-100" onclick="generarReporteAlertas()">
                                                                        <i class="fas fa-chart-bar me-2"></i>Generar Reporte de Alertas
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Activos -->
                    <div class="tab-pane fade" id="activos" role="tabpanel">
                        <!-- Submenú de Activos -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#activos-creacion">Creación</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#activos-depreciacion">Depreciación</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#activos-movimientos">Movimientos</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#activos-reportes">Reportes</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#activos-integracion">Integración</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Creación -->
                            <div class="tab-pane fade show active" id="activos-creacion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header activos">
                                                <i class="fas fa-plus-circle me-2"></i>Creación de Activos Fijos
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-6">
                                                        <button class="btn btn-activos" onclick="mostrarModalNuevoActivo()">
                                                            <i class="fas fa-plus me-2"></i>Nuevo Activo
                                                        </button>
                                                        <button class="btn btn-outline-secondary ms-2" onclick="exportarCatalogoActivos()">
                                                            <i class="fas fa-download me-2"></i>Exportar Catálogo
                                                        </button>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="search-box">
                                                            <i class="fas fa-search search-icon"></i>
                                                            <input type="text" id="searchActivos" class="form-control" placeholder="Buscar activos...">
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row" id="listaActivos">
                                                    <!-- Los activos se cargarán aquí como tarjetas -->
                                                    <div class="col-md-12 text-center py-4">
                                                        <i class="fas fa-cubes fa-3x text-muted mb-3"></i>
                                                        <h5>No hay activos registrados</h5>
                                                        <p class="text-muted">Comience creando su primer activo fijo</p>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Total Activos</h6>
                                                                <div class="metric-value" id="totalActivos">0</div>
                                                                <div class="metric-unit">Activos registrados</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Valor Total</h6>
                                                                <div class="metric-value" id="valorTotalActivos">$0.00</div>
                                                                <div class="metric-unit">USD</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Depreciación Acumulada</h6>
                                                                <div class="metric-value" id="depreciacionAcumulada">$0.00</div>
                                                                <div class="metric-unit">USD</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Valor Neto</h6>
                                                                <div class="metric-value" id="valorNetoActivos">$0.00</div>
                                                                <div class="metric-unit">USD</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Depreciación -->
                            <div class="tab-pane fade" id="activos-depreciacion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header activos">
                                                <i class="fas fa-chart-line me-2"></i>Gestión de Depreciación
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Método de Depreciación</h6>
                                                                <select class="form-select" id="selectMetodoDepreciacion">
                                                                    <option value="linea-recta">Línea Recta</option>
                                                                    <option value="unidades-produccion">Unidades de Producción</option>
                                                                    <option value="acelerada">Acelerada</option>
                                                                </select>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-8">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Simulación de Depreciación</h6>
                                                                <div class="row">
                                                                    <div class="col-md-4">
                                                                        <label class="form-label">Valor Adquisición</label>
                                                                        <input type="number" class="form-control" id="simValorAdquisicion" value="10000" step="0.01">
                                                                    </div>
                                                                    <div class="col-md-4">
                                                                        <label class="form-label">Vida Útil (años)</label>
                                                                        <input type="number" class="form-control" id="simVidaUtil" value="5" min="1">
                                                                    </div>
                                                                    <div class="col-md-4">
                                                                        <label class="form-label">Valor Residual</label>
                                                                        <input type="number" class="form-control" id="simValorResidual" value="1000" step="0.01">
                                                                    </div>
                                                                </div>
                                                                <div class="row mt-2">
                                                                    <div class="col-md-12">
                                                                        <button class="btn btn-activos" onclick="simularDepreciacion()">
                                                                            <i class="fas fa-calculator me-2"></i>Simular Depreciación
                                                                        </button>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Depreciación Mensual</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm depreciation-table">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Activo</th>
                                                                                <th>Valor Adquisición</th>
                                                                                <th>Depreciación Mensual USD</th>
                                                                                <th>Depreciación Mensual Bs</th>
                                                                                <th>Depreciación Acumulada</th>
                                                                                <th>Valor Neto</th>
                                                                                <th>Acción</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaDepreciacionMensual">
                                                                            <tr>
                                                                                <td colspan="7" class="text-center">No hay activos con depreciación calculada</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                                <div class="mt-3">
                                                                    <button class="btn btn-activos" onclick="calcularDepreciacionMensual()">
                                                                        <i class="fas fa-calculator me-2"></i>Calcular Depreciación Mensual
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Reporte de Depreciación</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoDepreciacion"></canvas>
                                                                </div>
                                                                <div class="mt-3">
                                                                    <button class="btn btn-info" onclick="exportarReporteDepreciacion()">
                                                                        <i class="fas fa-file-excel me-2"></i>Exportar Reporte de Depreciación
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Movimientos -->
                            <div class="tab-pane fade" id="activos-movimientos">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header activos">
                                                <i class="fas fa-exchange-alt me-2"></i>Movimientos de Activos
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-12 text-end">
                                                        <button class="btn btn-activos" onclick="mostrarModalNuevoMovimientoActivo()">
                                                            <i class="fas fa-plus me-2"></i>Nuevo Movimiento
                                                        </button>
                                                    </div>
                                                </div>
                                                
                                                <div class="table-responsive">
                                                    <table class="table table-hover">
                                                        <thead>
                                                            <tr>
                                                                <th>Fecha</th>
                                                                <th>Tipo Movimiento</th>
                                                                <th>Activo</th>
                                                                <th>Descripción</th>
                                                                <th>Valor USD</th>
                                                                <th>Valor Bs</th>
                                                                <th>Responsable</th>
                                                                <th>Acciones</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaMovimientosActivos">
                                                            <tr>
                                                                <td colspan="8" class="text-center">No hay movimientos registrados</td>
                                                            </tr>
                                                        </tbody>
                                                    </table>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-6">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Tipos de Movimiento</h6>
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <div class="metric-value" id="totalTransferencias">0</div>
                                                                        <div class="metric-unit">Transferencias</div>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <div class="metric-value" id="totalRevalorizaciones">0</div>
                                                                        <div class="metric-unit">Revalorizaciones</div>
                                                                    </div>
                                                                </div>
                                                                <div class="row mt-3">
                                                                    <div class="col-md-6">
                                                                        <div class="metric-value" id="totalBajas">0</div>
                                                                        <div class="metric-unit">Bajas</div>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <div class="metric-value" id="totalMantenimientos">0</div>
                                                                        <div class="metric-unit">Mantenimientos</div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Valorización de Activos</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoValorizacionActivos"></canvas>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Reportes -->
                            <div class="tab-pane fade" id="activos-reportes">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header activos">
                                                <i class="fas fa-file-alt me-2"></i>Reportes de Activos Fijos
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Inventario de Activos</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Categoría</th>
                                                                                <th>Cantidad</th>
                                                                                <th>Valor Total USD</th>
                                                                                <th>% del Total</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaInventarioActivos">
                                                                            <tr>
                                                                                <td>Maquinaria</td>
                                                                                <td>0</td>
                                                                                <td>$0.00</td>
                                                                                <td>0%</td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Vehículos</td>
                                                                                <td>0</td>
                                                                                <td>$0.00</td>
                                                                                <td>0%</td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Edificios</td>
                                                                                <td>0</td>
                                                                                <td>$0.00</td>
                                                                                <td>0%</td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Equipos</td>
                                                                                <td>0</td>
                                                                                <td>$0.00</td>
                                                                                <td>0%</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Participación en Costos</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoParticipacionActivos"></canvas>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Alertas de Activos</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Tipo Alerta</th>
                                                                                <th>Activo</th>
                                                                                <th>Descripción</th>
                                                                                <th>Fecha</th>
                                                                                <th>Estado</th>
                                                                                <th>Acción</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaAlertasActivos">
                                                                            <tr>
                                                                                <td colspan="6" class="text-center">No hay alertas activas</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Exportación de Reportes</h6>
                                                                <div class="export-buttons">
                                                                    <button class="btn btn-success" onclick="exportarReporteActivosExcel()">
                                                                        <i class="fas fa-file-excel me-2"></i>Inventario Excel
                                                                    </button>
                                                                    <button class="btn btn-danger" onclick="exportarReporteActivosPDF()">
                                                                        <i class="fas fa-file-pdf me-2"></i>Reporte PDF
                                                                    </button>
                                                                    <button class="btn btn-info" onclick="exportarDepreciacionCompleta()">
                                                                        <i class="fas fa-chart-line me-2"></i>Depreciación
                                                                    </button>
                                                                    <button class="btn btn-warning" onclick="exportarMovimientosActivos()">
                                                                        <i class="fas fa-exchange-alt me-2"></i>Movimientos
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Integración -->
                            <div class="tab-pane fade" id="activos-integracion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header activos">
                                                <i class="fas fa-link me-2"></i>Integración con Otros Módulos
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6><i class="fas fa-industry me-2"></i>Producción</h6>
                                                                <p>Depreciación de maquinaria se carga como costo indirecto de producción.</p>
                                                                <div class="metric-value" id="depreciacionProduccion">$0.00</div>
                                                                <div class="metric-unit">Depreciación mensual producción</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6><i class="fas fa-tools me-2"></i>Servicios</h6>
                                                                <p>Vehículos y equipos de vigilancia integrados al costo de transporte y seguridad.</p>
                                                                <div class="metric-value" id="depreciacionServicios">$0.00</div>
                                                                <div class="metric-unit">Depreciación mensual servicios</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6><i class="fas fa-file-invoice-dollar me-2"></i>Impuestos</h6>
                                                                <p>Activos influyen en cálculos fiscales y exoneraciones por inversión.</p>
                                                                <div class="metric-value" id="impactoFiscalActivos">$0.00</div>
                                                                <div class="metric-unit">Impacto fiscal anual</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6><i class="fas fa-chart-bar me-2"></i>Reportes</h6>
                                                                <p>Cada activo aparece con su ficha y depreciación en reportes consolidados.</p>
                                                                <div class="metric-value" id="participacionActivosReportes">0%</div>
                                                                <div class="metric-unit">Participación en costos totales</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Flujo de Integración</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Módulo Origen</th>
                                                                                <th>Módulo Destino</th>
                                                                                <th>Datos Compartidos</th>
                                                                                <th>Frecuencia</th>
                                                                                <th>Estado</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaFlujoIntegracion">
                                                                            <tr>
                                                                                <td>Activos Fijos</td>
                                                                                <td>Producción</td>
                                                                                <td>Depreciación maquinaria</td>
                                                                                <td>Mensual</td>
                                                                                <td><span class="badge bg-success">Activo</span></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Activos Fijos</td>
                                                                                <td>Servicios</td>
                                                                                <td>Depreciación vehículos</td>
                                                                                <td>Mensual</td>
                                                                                <td><span class="badge bg-success">Activo</span></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Activos Fijos</td>
                                                                                <td>Impuestos</td>
                                                                                <td>Valor activos para cálculo</td>
                                                                                <td>Anual</td>
                                                                                <td><span class="badge bg-warning">Pendiente</span></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Activos Fijos</td>
                                                                                <td>Reportes</td>
                                                                                <td>Ficha técnica y financiera</td>
                                                                                <td>Mensual</td>
                                                                                <td><span class="badge bg-success">Activo</span></td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Compras -->
                    <div class="tab-pane fade" id="compras" role="tabpanel">
                        <!-- Submenú de Compras -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#compras-proveedores">Proveedores</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#compras-ordenes">Órdenes</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#compras-exportacion">Exportación</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#compras-reportes">Reportes</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#compras-integracion">Integración</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Proveedores -->
                            <div class="tab-pane fade show active" id="compras-proveedores">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header compras">
                                                <i class="fas fa-address-book me-2"></i>Submódulo de Proveedores
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-6">
                                                        <button class="btn btn-compras" onclick="mostrarModalNuevoProveedor()">
                                                            <i class="fas fa-plus me-2"></i>Nuevo Proveedor
                                                        </button>
                                                        <button class="btn btn-outline-secondary ms-2" onclick="exportarCatalogoProveedores()">
                                                            <i class="fas fa-download me-2"></i>Exportar Catálogo
                                                        </button>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="search-box">
                                                            <i class="fas fa-search search-icon"></i>
                                                            <input type="text" id="searchProveedores" class="form-control" placeholder="Buscar proveedores...">
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row" id="listaProveedores">
                                                    <!-- Los proveedores se cargarán aquí como tarjetas -->
                                                    <div class="col-md-12 text-center py-4">
                                                        <i class="fas fa-building fa-3x text-muted mb-3"></i>
                                                        <h5>No hay proveedores registrados</h5>
                                                        <p class="text-muted">Comience registrando su primer proveedor</p>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Total Proveedores</h6>
                                                                <div class="metric-value" id="totalProveedores">0</div>
                                                                <div class="metric-unit">Proveedores registrados</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Proveedores Activos</h6>
                                                                <div class="metric-value" id="proveedoresActivos">0</div>
                                                                <div class="metric-unit">Activos</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Compras Totales</h6>
                                                                <div class="metric-value" id="comprasTotalesProveedores">$0.00</div>
                                                                <div class="metric-unit">USD</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Órdenes Activas</h6>
                                                                <div class="metric-value" id="ordenesActivasProveedores">0</div>
                                                                <div class="metric-unit">Órdenes</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Órdenes -->
                            <div class="tab-pane fade" id="compras-ordenes">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header compras">
                                                <i class="fas fa-file-purchase-order me-2"></i>Registro de Órdenes de Compra/Servicio
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-12 text-end">
                                                        <button class="btn btn-compras" onclick="mostrarModalNuevaOrden()">
                                                            <i class="fas fa-plus me-2"></i>Nueva Orden
                                                        </button>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mb-3">
                                                    <div class="col-md-3">
                                                        <select class="form-select" id="filterEstadoOrden">
                                                            <option value="">Todos los estados</option>
                                                            <option value="pendiente">Pendiente</option>
                                                            <option value="aprobada">Aprobada</option>
                                                            <option value="rechazada">Rechazada</option>
                                                            <option value="completada">Completada</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <select class="form-select" id="filterProveedorOrden">
                                                            <option value="">Todos los proveedores</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <select class="form-select" id="filterCentroCostoOrden">
                                                            <option value="">Todos los centros</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <input type="date" class="form-control" id="filterFechaOrden">
                                                    </div>
                                                </div>
                                                
                                                <div class="table-responsive">
                                                    <table class="table table-hover">
                                                        <thead>
                                                            <tr>
                                                                <th>Número</th>
                                                                <th>Fecha</th>
                                                                <th>Proveedor</th>
                                                                <th>Centro Costo</th>
                                                                <th>Elemento Costo</th>
                                                                <th>Monto USD</th>
                                                                <th>Monto Bs</th>
                                                                <th>Estado</th>
                                                                <th>Acciones</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaOrdenesCompras">
                                                            <tr>
                                                                <td colspan="9" class="text-center">No hay órdenes registradas</td>
                                                            </tr>
                                                        </tbody>
                                                    </table>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Órdenes Pendientes</h6>
                                                                <div class="metric-value" id="ordenesPendientes">0</div>
                                                                <div class="metric-unit">Órdenes</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Valor Pendiente</h6>
                                                                <div class="metric-value" id="valorPendienteOrdenes">$0.00</div>
                                                                <div class="metric-unit">USD</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Órdenes este Mes</h6>
                                                                <div class="metric-value" id="ordenesEsteMes">0</div>
                                                                <div class="metric-unit">Órdenes</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Exportación -->
                            <div class="tab-pane fade" id="compras-exportacion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header compras">
                                                <i class="fas fa-download me-2"></i>Exportación Masiva
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6><i class="fas fa-file-excel text-success me-2"></i>Exportar Órdenes</h6>
                                                                <p>Exporte todas las órdenes de un período a Excel/PDF con metadatos.</p>
                                                                
                                                                <div class="mt-3">
                                                                    <label class="form-label">Seleccionar Período</label>
                                                                    <select class="form-select" id="selectPeriodoExportOrdenes">
                                                                        <option value="actual">Período Actual</option>
                                                                        <!-- Se llenará dinámicamente -->
                                                                    </select>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <label class="form-label">Filtros Adicionales</label>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkFiltrarProveedor">
                                                                        <label class="form-check-label" for="checkFiltrarProveedor">
                                                                            Filtrar por proveedor
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkFiltrarCentro">
                                                                        <label class="form-check-label" for="checkFiltrarCentro">
                                                                            Filtrar por centro de costo
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkFiltrarElemento">
                                                                        <label class="form-check-label" for="checkFiltrarElemento">
                                                                            Filtrar por elemento de costo
                                                                        </label>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <button class="btn btn-success w-100" onclick="exportarOrdenesExcel()">
                                                                        <i class="fas fa-file-excel me-2"></i>Exportar a Excel
                                                                    </button>
                                                                    <button class="btn btn-danger w-100 mt-2" onclick="exportarOrdenesPDF()">
                                                                        <i class="fas fa-file-pdf me-2"></i>Exportar a PDF
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6><i class="fas fa-address-card text-primary me-2"></i>Exportar Proveedores</h6>
                                                                <p>Exporte catálogo completo de proveedores con códigos, RIF, nombre y estado.</p>
                                                                
                                                                <div class="mt-3">
                                                                    <label class="form-label">Formato de Exportación</label>
                                                                    <select class="form-select" id="selectFormatoProveedores">
                                                                        <option value="excel">Excel (.xlsx)</option>
                                                                        <option value="pdf">PDF (.pdf)</option>
                                                                        <option value="csv">CSV (.csv)</option>
                                                                    </select>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <label class="form-label">Campos a Incluir</label>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkIncluirCodigo" checked>
                                                                        <label class="form-check-label" for="checkIncluirCodigo">
                                                                            Código automático
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkIncluirRIF" checked>
                                                                        <label class="form-check-label" for="checkIncluirRIF">
                                                                            RIF
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkIncluirContacto" checked>
                                                                        <label class="form-check-label" for="checkIncluirContacto">
                                                                            Contacto
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkIncluirCompras">
                                                                        <label class="form-check-label" for="checkIncluirCompras">
                                                                            Histórico de compras
                                                                        </label>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <button class="btn btn-primary w-100" onclick="exportarProveedores()">
                                                                        <i class="fas fa-download me-2"></i>Exportar Proveedores
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6><i class="fas fa-upload text-warning me-2"></i>Importación Masiva</h6>
                                                                <p>Importe datos desde archivos Excel o CSV.</p>
                                                                
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Tipo de Importación</label>
                                                                            <select class="form-select" id="selectTipoImportacion">
                                                                                <option value="proveedores">Proveedores</option>
                                                                                <option value="ordenes">Órdenes de Compra</option>
                                                                                <option value="items">Ítems de Orden</option>
                                                                            </select>
                                                                        </div>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Archivo a Importar</label>
                                                                            <input type="file" class="form-control" id="fileImportacion" accept=".xlsx,.xls,.csv">
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <button class="btn btn-warning w-100" onclick="importarDatosCompras()">
                                                                        <i class="fas fa-upload me-2"></i>Importar Datos
                                                                    </button>
                                                                    <small class="text-muted d-block mt-2">Formatos soportados: Excel (.xlsx, .xls), CSV (.csv)</small>
                                                                </div>
                                                                
                                                                <div class="mt-3">
                                                                    <div class="alert alert-info">
                                                                        <i class="fas fa-info-circle me-2"></i>
                                                                        <strong>Nota:</strong> Descargue la plantilla de importación para asegurar el formato correcto.
                                                                        <button class="btn btn-sm btn-outline-info ms-2" onclick="descargarPlantillaImportacion()">
                                                                            <i class="fas fa-download me-1"></i>Descargar Plantilla
                                                                        </button>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Reportes -->
                            <div class="tab-pane fade" id="compras-reportes">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header compras">
                                                <i class="fas fa-chart-bar me-2"></i>Reportes del Módulo
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Consolidado por Proveedor</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoConsolidadoProveedor"></canvas>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Consolidado por Centro/Elemento</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoConsolidadoCentro"></canvas>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Histórico de Precios Unitarios</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Ítem/Servicio</th>
                                                                                <th>Proveedor</th>
                                                                                <th>Precio Actual USD</th>
                                                                                <th>Precio Anterior USD</th>
                                                                                <th>Variación %</th>
                                                                                <th>Tendencia</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaHistoricoPrecios">
                                                                            <tr>
                                                                                <td colspan="6" class="text-center">No hay datos históricos</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Alertas del Sistema</h6>
                                                                <div id="alertasComprasContainer">
                                                                    <div class="alert alert-warning">
                                                                        <i class="fas fa-exclamation-triangle me-2"></i>
                                                                        <strong>Órdenes Duplicadas:</strong> No se detectaron órdenes duplicadas
                                                                    </div>
                                                                    <div class="alert alert-info">
                                                                        <i class="fas fa-info-circle me-2"></i>
                                                                        <strong>Proveedores Inactivos:</strong> No hay proveedores inactivos
                                                                    </div>
                                                                    <div class="alert alert-success">
                                                                        <i class="fas fa-check-circle me-2"></i>
                                                                        <strong>Compras dentro de Presupuesto:</strong> Todas las compras están dentro del presupuesto
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Exportación de Reportes</h6>
                                                                <div class="export-buttons">
                                                                    <button class="btn btn-success" onclick="exportarReporteConsolidadoProveedor()">
                                                                        <i class="fas fa-file-excel me-2"></i>Consolidado Proveedor
                                                                    </button>
                                                                    <button class="btn btn-primary" onclick="exportarReporteConsolidadoCentro()">
                                                                        <i class="fas fa-file-excel me-2"></i>Consolidado Centro
                                                                    </button>
                                                                    <button class="btn btn-info" onclick="exportarHistoricoPrecios()">
                                                                        <i class="fas fa-chart-line me-2"></i>Histórico Precios
                                                                    </button>
                                                                    <button class="btn btn-warning" onclick="exportarAlertasCompras()">
                                                                        <i class="fas fa-bell me-2"></i>Reporte Alertas
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Integración -->
                            <div class="tab-pane fade" id="compras-integracion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header compras">
                                                <i class="fas fa-network-wired me-2"></i>Integración con Otros Módulos
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-warehouse fa-3x text-almacen mb-3"></i>
                                                                <h6>Almacén</h6>
                                                                <p>Cada orden aprobada genera una entrada de inventario automáticamente.</p>
                                                                <div class="metric-value" id="entradasGeneradas">0</div>
                                                                <div class="metric-unit">Entradas generadas</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-industry fa-3x text-produccion mb-3"></i>
                                                                <h6>Producción/Servicios</h6>
                                                                <p>Las salidas de almacén se vinculan con las compras registradas.</p>
                                                                <div class="metric-value" id="salidasVinculadas">0</div>
                                                                <div class="metric-unit">Salidas vinculadas</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-file-invoice-dollar fa-3x text-impuestos mb-3"></i>
                                                                <h6>Impuestos</h6>
                                                                <p>Compras sujetas a IVA u otros tributos se reflejan en el módulo de impuestos.</p>
                                                                <div class="metric-value" id="comprasConIVA">0</div>
                                                                <div class="metric-unit">Compras con IVA</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Flujo de Datos entre Módulos</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Módulo Origen</th>
                                                                                <th>Módulo Destino</th>
                                                                                <th>Datos Transferidos</th>
                                                                                <th>Trigger/Evento</th>
                                                                                <th>Estado</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaFlujoDatosCompras">
                                                                            <tr>
                                                                                <td>Compras</td>
                                                                                <td>Almacén</td>
                                                                                <td>Orden aprobada → Entrada inventario</td>
                                                                                <td>Aprobación de orden</td>
                                                                                <td><span class="badge bg-success">Activo</span></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Compras</td>
                                                                                <td>Cuentas por Pagar</td>
                                                                                <td>Orden → Factura por pagar</td>
                                                                                <td>Recepción de factura</td>
                                                                                <td><span class="badge bg-success">Activo</span></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Compras</td>
                                                                                <td>Reportes</td>
                                                                                <td>Cada orden en consolidado</td>
                                                                                <td>Cierre de período</td>
                                                                                <td><span class="badge bg-success">Activo</span></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Compras</td>
                                                                                <td>Impuestos</td>
                                                                                <td>IVA de compras</td>
                                                                                <td>Registro de factura</td>
                                                                                <td><span class="badge bg-warning">Pendiente</span></td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Validaciones Cruzadas</h6>
                                                                <div class="row">
                                                                    <div class="col-md-4">
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkValidarProveedorActivo" checked>
                                                                            <label class="form-check-label" for="checkValidarProveedorActivo">
                                                                                Validar proveedor activo
                                                                            </label>
                                                                        </div>
                                                                    </div>
                                                                    <div class="col-md-4">
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkValidarPresupuesto" checked>
                                                                            <label class="form-check-label" for="checkValidarPresupuesto">
                                                                                Validar contra presupuesto
                                                                            </label>
                                                                        </div>
                                                                    </div>
                                                                    <div class="col-md-4">
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkValidarDuplicados" checked>
                                                                            <label class="form-check-label" for="checkValidarDuplicados">
                                                                                Validar órdenes duplicadas
                                                                            </label>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="row mt-2">
                                                                    <div class="col-md-4">
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkValidarPeriodoAbierto" checked>
                                                                            <label class="form-check-label" for="checkValidarPeriodoAbierto">
                                                                                Validar período contable abierto
                                                                            </label>
                                                                        </div>
                                                                    </div>
                                                                    <div class="col-md-4">
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkValidarAprobaciones" checked>
                                                                            <label class="form-check-label" for="checkValidarAprobaciones">
                                                                                Validar flujo de aprobaciones
                                                                            </label>
                                                                        </div>
                                                                    </div>
                                                                    <div class="col-md-4">
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkValidarDocumentacion" checked>
                                                                            <label class="form-check-label" for="checkValidarDocumentacion">
                                                                                Validar documentación completa
                                                                            </label>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="mt-3">
                                                                    <button class="btn btn-compras" onclick="guardarConfiguracionValidaciones()">
                                                                        <i class="fas fa-save me-2"></i>Guardar Configuración de Validaciones
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Cuentas por Pagar -->
                    <div class="tab-pane fade" id="cuentas-pagar" role="tabpanel">
                        <!-- Submenú de Cuentas por Pagar -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#cxp-flujo">Flujo Lógico</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#cxp-registro">Registro</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#cxp-reportes">Reportes</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#cxp-integracion">Integración</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Flujo Lógico -->
                            <div class="tab-pane fade show active" id="cxp-flujo">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header cuentas-pagar">
                                                <i class="fas fa-project-diagram me-2"></i>Flujo Lógico de Cuentas por Pagar
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-12">
                                                        <div class="alert alert-info">
                                                            <h6><i class="fas fa-info-circle me-2"></i>Descripción del Flujo</h6>
                                                            <p class="mb-0">Cada orden registrada en Compras o Servicios se transfiere automáticamente a CxP. Luego se completa con información de factura, se calcula IVA automáticamente y se registra como cuenta por pagar.</p>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-3">
                                                        <div class="card text-center">
                                                            <div class="card-body">
                                                                <div class="step-number">1</div>
                                                                <h6>Carga Automática</h6>
                                                                <p class="small">Órdenes de Compras/Servicios se transfieren a CxP</p>
                                                                <div class="metric-value" id="cargasAutomaticas">0</div>
                                                                <div class="metric-unit">Órdenes transferidas</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-3">
                                                        <div class="card text-center">
                                                            <div class="card-body">
                                                                <div class="step-number">2</div>
                                                                <h6>Registro de Factura</h6>
                                                                <p class="small">Se completa información de factura y se calcula IVA</p>
                                                                <div class="metric-value" id="facturasRegistradas">0</div>
                                                                <div class="metric-unit">Facturas registradas</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-3">
                                                        <div class="card text-center">
                                                            <div class="card-body">
                                                                <div class="step-number">3</div>
                                                                <h6>Validaciones</h6>
                                                                <p class="small">Verificación de facturas duplicadas y cálculos correctos</p>
                                                                <div class="metric-value" id="validacionesExitosas">100%</div>
                                                                <div class="metric-unit">Tasa de éxito</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-3">
                                                        <div class="card text-center">
                                                            <div class="card-body">
                                                                <div class="step-number">4</div>
                                                                <h6>Estados</h6>
                                                                <p class="small">Seguimiento de estados: Pendiente, Parcial, Pagada, Vencida</p>
                                                                <div class="metric-value" id="facturasPendientes">0</div>
                                                                <div class="metric-unit">Facturas pendientes</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Campos del Submódulo</h6>
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <ul class="list-group">
                                                                            <li class="list-group-item d-flex justify-content-between align-items-center">
                                                                                Proveedor (nombre y código)
                                                                                <span class="badge bg-primary rounded-pill">Obligatorio</span>
                                                                            </li>
                                                                            <li class="list-group-item d-flex justify-content-between align-items-center">
                                                                                Factura (fecha, número, montos)
                                                                                <span class="badge bg-primary rounded-pill">Obligatorio</span>
                                                                            </li>
                                                                            <li class="list-group-item d-flex justify-content-between align-items-center">
                                                                                Centro de costo
                                                                                <span class="badge bg-primary rounded-pill">Obligatorio</span>
                                                                            </li>
                                                                            <li class="list-group-item d-flex justify-content-between align-items-center">
                                                                                Elemento de costo
                                                                                <span class="badge bg-primary rounded-pill">Obligatorio</span>
                                                                            </li>
                                                                        </ul>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <ul class="list-group">
                                                                            <li class="list-group-item d-flex justify-content-between align-items-center">
                                                                                Moneda (USD/Bs)
                                                                                <span class="badge bg-primary rounded-pill">Obligatorio</span>
                                                                            </li>
                                                                            <li class="list-group-item d-flex justify-content-between align-items-center">
                                                                                Tasa BCV utilizada
                                                                                <span class="badge bg-primary rounded-pill">Obligatorio</span>
                                                                            </li>
                                                                            <li class="list-group-item d-flex justify-content-between align-items-center">
                                                                                Responsable
                                                                                <span class="badge bg-primary rounded-pill">Obligatorio</span>
                                                                            </li>
                                                                            <li class="list-group-item d-flex justify-content-between align-items-center">
                                                                                Estado de la cuenta
                                                                                <span class="badge bg-primary rounded-pill">Obligatorio</span>
                                                                            </li>
                                                                        </ul>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Registro -->
                            <div class="tab-pane fade" id="cxp-registro">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header cuentas-pagar">
                                                <i class="fas fa-file-invoice me-2"></i>Registro de Facturas
                                            </div>
                                            <div class="card-body">
                                                <div class="row mb-3">
                                                    <div class="col-md-12 text-end">
                                                        <button class="btn btn-cuentas-pagar" onclick="mostrarModalNuevaFactura()">
                                                            <i class="fas fa-plus me-2"></i>Nueva Factura
                                                        </button>
                                                        <button class="btn btn-outline-secondary ms-2" onclick="cargarOrdenesPendientes()">
                                                            <i class="fas fa-sync-alt me-2"></i>Cargar Órdenes Pendientes
                                                        </button>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mb-3">
                                                    <div class="col-md-3">
                                                        <select class="form-select" id="filterEstadoFactura">
                                                            <option value="">Todos los estados</option>
                                                            <option value="pendiente">Pendiente</option>
                                                            <option value="parcial">Parcialmente Pagada</option>
                                                            <option value="pagada">Pagada</option>
                                                            <option value="vencida">Vencida</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <select class="form-select" id="filterProveedorFactura">
                                                            <option value="">Todos los proveedores</option>
                                                        </select>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <input type="date" class="form-control" id="filterFechaVencimientoDesde" placeholder="Vencimiento desde">
                                                    </div>
                                                    <div class="col-md-3">
                                                        <input type="date" class="form-control" id="filterFechaVencimientoHasta" placeholder="Vencimiento hasta">
                                                    </div>
                                                </div>
                                                
                                                <div class="table-responsive">
                                                    <table class="table table-hover">
                                                        <thead>
                                                            <tr>
                                                                <th>Factura</th>
                                                                <th>Proveedor</th>
                                                                <th>Fecha</th>
                                                                <th>Vencimiento</th>
                                                                <th>Base Imponible</th>
                                                                <th>IVA</th>
                                                                <th>Total</th>
                                                                <th>Estado</th>
                                                                <th>Acciones</th>
                                                            </tr>
                                                        </thead>
                                                        <tbody id="tablaFacturas">
                                                            <tr>
                                                                <td colspan="9" class="text-center">No hay facturas registradas</td>
                                                            </tr>
                                                        </tbody>
                                                    </table>
                                                </div>
                                                
                                                <div class="row mt-4">
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Total Pendiente</h6>
                                                                <div class="metric-value" id="totalPendienteFacturas">$0.00</div>
                                                                <div class="metric-unit">USD</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Facturas Vencidas</h6>
                                                                <div class="metric-value" id="facturasVencidas">0</div>
                                                                <div class="metric-unit">Facturas</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>IVA por Pagar</h6>
                                                                <div class="metric-value" id="ivaPorPagar">$0.00</div>
                                                                <div class="metric-unit">USD</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-3">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Próximo Vencimiento</h6>
                                                                <div class="metric-value" id="proximoVencimientoFacturas">--/--</div>
                                                                <div class="metric-unit">Fecha</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Reportes -->
                            <div class="tab-pane fade" id="cxp-reportes">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header cuentas-pagar">
                                                <i class="fas fa-chart-pie me-2"></i>Reportes de Cuentas por Pagar
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Consolidado por Proveedor</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoConsolidadoProveedorCXP"></canvas>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Consolidado por Centro de Costo</h6>
                                                                <div class="chart-container">
                                                                    <canvas id="graficoConsolidadoCentroCXP"></canvas>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Histórico de Pagos</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Factura</th>
                                                                                <th>Proveedor</th>
                                                                                <th>Fecha Pago</th>
                                                                                <th>Monto Pagado USD</th>
                                                                                <th>Monto Pagado Bs</th>
                                                                                <th>Tasa BCV</th>
                                                                                <th>Método Pago</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaHistoricoPagos">
                                                                            <tr>
                                                                                <td colspan="7" class="text-center">No hay pagos registrados</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Alertas de Vencimiento</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Factura</th>
                                                                                <th>Proveedor</th>
                                                                                <th>Fecha Vencimiento</th>
                                                                                <th>Días Restantes</th>
                                                                                <th>Monto USD</th>
                                                                                <th>Estado</th>
                                                                                <th>Acción</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaAlertasVencimientoCXP">
                                                                            <tr>
                                                                                <td colspan="7" class="text-center">No hay alertas de vencimiento</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Consolidado Final</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Proveedor</th>
                                                                                <th>Factura</th>
                                                                                <th>Descripción</th>
                                                                                <th>Monto sin IVA USD</th>
                                                                                <th>Tasa de Cambio</th>
                                                                                <th>Total en Bs sin IVA</th>
                                                                                <th>Observación</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaConsolidadoFinalCXP">
                                                                            <tr>
                                                                                <td colspan="7" class="text-center">No hay datos para consolidado</td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Exportación de Reportes</h6>
                                                                <div class="export-buttons">
                                                                    <button class="btn btn-success" onclick="exportarReporteFacturasExcel()">
                                                                        <i class="fas fa-file-excel me-2"></i>Reporte Facturas Excel
                                                                    </button>
                                                                    <button class="btn btn-danger" onclick="exportarReporteFacturasPDF()">
                                                                        <i class="fas fa-file-pdf me-2"></i>Reporte Facturas PDF
                                                                    </button>
                                                                    <button class="btn btn-primary" onclick="exportarConsolidadoFinal()">
                                                                        <i class="fas fa-list-alt me-2"></i>Consolidado Final
                                                                    </button>
                                                                    <button class="btn btn-warning" onclick="previewFacturaPDF()">
                                                                        <i class="fas fa-eye me-2"></i>Vista Previa Factura
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Integración -->
                            <div class="tab-pane fade" id="cxp-integracion">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header cuentas-pagar">
                                                <i class="fas fa-link me-2"></i>Integración del Sistema
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-shopping-cart fa-3x text-compras mb-3"></i>
                                                                <h6>Compras/Servicios</h6>
                                                                <p>Cada orden aprobada genera automáticamente una cuenta por pagar.</p>
                                                                <div class="metric-value" id="ordenesConvertidasCXP">0</div>
                                                                <div class="metric-unit">Órdenes convertidas</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-cogs fa-3x text-configuracion mb-3"></i>
                                                                <h6>Configuración</h6>
                                                                <p>IVA configurable (por defecto 16%). Validaciones automáticas.</p>
                                                                <div class="metric-value" id="ivaConfigurado">16%</div>
                                                                <div class="metric-unit">Tasa IVA actual</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-chart-bar fa-3x text-reportes mb-3"></i>
                                                                <h6>Reportes</h6>
                                                                <p>Cada factura aparece en reportes con proveedor, centro, elemento, montos.</p>
                                                                <div class="metric-value" id="facturasEnReportes">0</div>
                                                                <div class="metric-unit">Facturas reportadas</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Automatización del IVA</h6>
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Porcentaje de IVA (%)</label>
                                                                            <div class="input-group">
                                                                                <input type="number" class="form-control" id="porcentajeIVA" value="16" step="0.01" min="0" max="100">
                                                                                <span class="input-group-text">%</span>
                                                                            </div>
                                                                            <small class="text-muted">Porcentaje de IVA aplicable por defecto</small>
                                                                        </div>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Base Imponible</label>
                                                                            <div class="input-group">
                                                                                <input type="number" class="form-control" id="baseImponibleCalculo" value="1000" step="0.01" min="0">
                                                                                <span class="input-group-text">USD</span>
                                                                            </div>
                                                                            <small class="text-muted">Ingrese la base imponible para calcular</small>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="row">
                                                                    <div class="col-md-12">
                                                                        <div class="card">
                                                                            <div class="card-body">
                                                                                <h6>Cálculo Automático</h6>
                                                                                <div class="row">
                                                                                    <div class="col-md-4">
                                                                                        <div class="metric-value" id="calculadoBaseImponible">$1,000.00</div>
                                                                                        <div class="metric-unit">Base Imponible</div>
                                                                                    </div>
                                                                                    <div class="col-md-4">
                                                                                        <div class="metric-value" id="calculadoIVA">$160.00</div>
                                                                                        <div class="metric-unit">IVA (16%)</div>
                                                                                    </div>
                                                                                    <div class="col-md-4">
                                                                                        <div class="metric-value" id="calculadoTotal">$1,160.00</div>
                                                                                        <div class="metric-unit">Total Factura</div>
                                                                                    </div>
                                                                                </div>
                                                                                <div class="mt-3">
                                                                                    <button class="btn btn-cuentas-pagar" onclick="calcularIVAAutomatico()">
                                                                                        <i class="fas fa-calculator me-2"></i>Calcular IVA Automáticamente
                                                                                    </button>
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Alertas Inteligentes</h6>
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkAlertasVencimientoCXP" checked>
                                                                            <label class="form-check-label" for="checkAlertasVencimientoCXP">
                                                                                Alertas de facturas próximas a vencer
                                                                            </label>
                                                                        </div>
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkAlertasProveedoresCriticos" checked>
                                                                            <label class="form-check-label" for="checkAlertasProveedoresCriticos">
                                                                                Alertas de proveedores críticos
                                                                            </label>
                                                                        </div>
                                                                        <div class="form-check">
                                                                            <input class="form-check-input" type="checkbox" id="checkAlertasMontosAltos">
                                                                            <label class="form-check-label" for="checkAlertasMontosAltos">
                                                                                Alertas de montos altos pendientes
                                                                            </label>
                                                                        </div>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Días para alerta de vencimiento</label>
                                                                            <input type="number" class="form-control" id="diasAlertaVencimiento" value="7" min="1" max="30">
                                                                        </div>
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Monto mínimo para alerta (USD)</label>
                                                                            <input type="number" class="form-control" id="montoMinimoAlerta" value="10000" step="0.01" min="0">
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="mt-3">
                                                                    <button class="btn btn-cuentas-pagar" onclick="guardarConfiguracionAlertasCXP()">
                                                                        <i class="fas fa-save me-2"></i>Guardar Configuración de Alertas
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Pestaña de Configuración -->
                    <div class="tab-pane fade" id="configuracion" role="tabpanel">
                        <!-- Submenú de Configuración -->
                        <div class="tab-submenu">
                            <ul class="nav">
                                <li class="nav-item">
                                    <a class="nav-link active" data-bs-toggle="tab" href="#config-parametros">Parámetros</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#config-catalogos">Catálogos</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#config-periodo">Período</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#config-roles">Roles</a>
                                </li>
                                <li class="nav-item">
                                    <a class="nav-link" data-bs-toggle="tab" href="#config-auditoria">Auditoría</a>
                                </li>
                            </ul>
                        </div>
                        
                        <div class="tab-content">
                            <!-- Subpestaña Parámetros -->
                            <div class="tab-pane fade show active" id="config-parametros">
                                <div class="row">
                                    <!-- Configuración de Tasas BCV -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-money-bill-wave me-2"></i>Tasas de Cambio
                                            </div>
                                            <div class="card-body">
                                                <div class="mb-3">
                                                    <label class="form-label">Tasa BCV (Bs por $1 USD)</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="configTasaBcv" step="0.0001" min="0" value="36.00" required>
                                                        <span class="input-group-text">Bs/$</span>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Tasa Euro a USD</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="configTasaEuro" step="0.0001" min="0" value="1.07" required>
                                                        <span class="input-group-text">USD/€</span>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Fecha de las Tasas</label>
                                                    <input type="date" class="form-control" id="configTasaFecha" value="" required>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Fuente de las Tasas</label>
                                                    <input type="text" class="form-control" id="configTasaFuente" value="BCV Oficial / BCE" required>
                                                </div>
                                                
                                                <div class="d-grid">
                                                    <button class="btn btn-configuracion" onclick="guardarConfiguracionTasa()">
                                                        <i class="fas fa-save me-2"></i>Guardar Tasas
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <!-- Configuración General -->
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-cog me-2"></i>Configuración General
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="mb-3">
                                                            <label class="form-label">Moneda Principal</label>
                                                            <select class="form-select" id="configMonedaPrincipal">
                                                                <option value="USD">Dólar Estadounidense (USD)</option>
                                                                <option value="BS">Bolívar Soberano (Bs)</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-6">
                                                        <div class="mb-3">
                                                            <label class="form-label">Formato de Fecha</label>
                                                            <select class="form-select" id="configFormatoFecha">
                                                                <option value="dd/mm/yyyy">DD/MM/YYYY</option>
                                                                <option value="mm/dd/yyyy">MM/DD/YYYY</option>
                                                                <option value="yyyy-mm-dd">YYYY-MM-DD</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="mb-3">
                                                            <label class="form-label">Zona Horaria</label>
                                                            <select class="form-select" id="configZonaHoraria">
                                                                <option value="America/Caracas">Venezuela (UTC-4)</option>
                                                                <option value="UTC">UTC</option>
                                                                <option value="America/New_York">EST (UTC-5)</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-6">
                                                        <div class="mb-3">
                                                            <label class="form-label">Responsable Período</label>
                                                            <input type="text" class="form-control" id="configResponsablePeriodo" placeholder="Nombre del responsable">
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="mb-3">
                                                            <label class="form-label">Decimales Montos</label>
                                                            <select class="form-select" id="configDecimalesMoneda">
                                                                <option value="2">2 decimales (0.00)</option>
                                                                <option value="3">3 decimales (0.000)</option>
                                                                <option value="4">4 decimales (0.0000)</option>
                                                                <option value="0">Sin decimales</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="mb-3">
                                                            <label class="form-label">Decimales Cantidades</label>
                                                            <select class="form-select" id="configDecimalesCantidad">
                                                                <option value="2">2 decimales (0.00)</option>
                                                                <option value="3">3 decimales (0.000)</option>
                                                                <option value="1">1 decimal (0.0)</option>
                                                                <option value="0">Sin decimales</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="mb-3">
                                                            <label class="form-label">Separador Decimal</label>
                                                            <select class="form-select" id="configSeparadorDecimal">
                                                                <option value=".">Punto (.)</option>
                                                                <option value=",">Coma (,)</option>
                                                            </select>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Separador de Miles</label>
                                                    <select class="form-select" id="configSeparadorMiles">
                                                        <option value=",">Coma (,)</option>
                                                        <option value=".">Punto (.)</option>
                                                        <option value=" ">Espacio ( )</option>
                                                        <option value="">Sin separador</option>
                                                    </select>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="row mt-3">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-sliders-h me-2"></i>Opciones del Sistema
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="mb-3 form-check">
                                                            <input type="checkbox" class="form-check-input" id="configAutoGuardar" checked>
                                                            <label class="form-check-label" for="configAutoGuardar">Auto-guardar cambios</label>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="mb-3 form-check">
                                                            <input type="checkbox" class="form-check-input" id="configNotificaciones" checked>
                                                            <label class="form-check-label" for="configNotificaciones">Mostrar notificaciones</label>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="mb-3 form-check">
                                                            <input type="checkbox" class="form-check-input" id="configAlertasVencimiento" checked>
                                                            <label class="form-check-label" for="configAlertasVencimiento">Alertas de vencimiento</label>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="mb-3 form-check">
                                                            <input type="checkbox" class="form-check-input" id="configValidarBlancos" checked>
                                                            <label class="form-check-label" for="configValidarBlancos">Validar campos en blanco (convertir a 0)</label>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="mb-3 form-check">
                                                            <input type="checkbox" class="form-check-input" id="configHabilitarCorrecciones">
                                                            <label class="form-check-label" for="configHabilitarCorrecciones">Habilitar notas de corrección</label>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="mb-3 form-check">
                                                            <input type="checkbox" class="form-check-input" id="configFirmaDigital" checked>
                                                            <label class="form-check-label" for="configFirmaDigital">Usar firma digital en reportes</label>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="d-grid gap-2 d-md-flex justify-content-md-end">
                                                    <button class="btn btn-success" onclick="guardarConfiguracionGeneral()">
                                                        <i class="fas fa-save me-2"></i>Guardar Configuración
                                                    </button>
                                                    <button class="btn btn-info" onclick="cargarConfiguracionPredeterminada()">
                                                        <i class="fas fa-redo me-2"></i>Cargar Configuración Predeterminada
                                                    </button>
                                                    <button class="btn btn-warning" onclick="exportarConfiguracion()">
                                                        <i class="fas fa-download me-2"></i>Exportar Configuración
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Catálogos -->
                            <div class="tab-pane fade" id="config-catalogos">
                                <div class="row">
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-list me-2"></i>Catálogos del Sistema
                                            </div>
                                            <div class="card-body">
                                                <div class="list-group">
                                                    <a href="#" class="list-group-item list-group-item-action d-flex justify-content-between align-items-center" onclick="mostrarModalCentrosCosto()">
                                                        Centros de Costo
                                                        <span class="badge bg-primary rounded-pill" id="badgeCentrosCosto">0</span>
                                                    </a>
                                                    <a href="#" class="list-group-item list-group-item-action d-flex justify-content-between align-items-center" onclick="mostrarModalElementosCosto()">
                                                        Elementos de Costo
                                                        <span class="badge bg-success rounded-pill" id="badgeElementosCosto">0</span>
                                                    </a>
                                                    <a href="#" class="list-group-item list-group-item-action d-flex justify-content-between align-items-center" onclick="mostrarModalClasificacionJerarquica()">
                                                        Clasificación Jerárquica
                                                        <span class="badge bg-info rounded-pill" id="badgeClasificacion">0</span>
                                                    </a>
                                                    <a href="#" class="list-group-item list-group-item-action d-flex justify-content-between align-items-center" onclick="mostrarModalInsumosAlmacen()">
                                                        Insumos de Almacén
                                                        <span class="badge bg-almacen rounded-pill" id="badgeInsumosAlmacen">0</span>
                                                    </a>
                                                    <a href="#" class="list-group-item list-group-item-action d-flex justify-content-between align-items-center" onclick="mostrarModalCategoriasActivos()">
                                                        Categorías de Activos
                                                        <span class="badge bg-activos rounded-pill" id="badgeCategoriasActivos">0</span>
                                                    </a>
                                                    <a href="#" class="list-group-item list-group-item-action d-flex justify-content-between align-items-center" onclick="mostrarModalProveedores()">
                                                        Proveedores
                                                        <span class="badge bg-compras rounded-pill" id="badgeProveedores">0</span>
                                                    </a>
                                                    <a href="#" class="list-group-item list-group-item-action d-flex justify-content-between align-items-center" onclick="mostrarModalMetodosDepreciacion()">
                                                        Métodos de Depreciación
                                                        <span class="badge bg-activos rounded-pill" id="badgeMetodosDepreciacion">0</span>
                                                    </a>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <button class="btn btn-outline-primary w-100" onclick="exportarTodosCatalogos()">
                                                        <i class="fas fa-download me-2"></i>Exportar Todos los Catálogos
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    
                                    <div class="col-md-6">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-database me-2"></i>Gestión de Datos
                                            </div>
                                            <div class="card-body">
                                                <div class="mb-3">
                                                    <label class="form-label">Backup Automático</label>
                                                    <select class="form-select" id="selectFrecuenciaBackup">
                                                        <option value="diario">Diario</option>
                                                        <option value="semanal" selected>Semanal</option>
                                                        <option value="mensual">Mensual</option>
                                                        <option value="nunca">Nunca</option>
                                                    </select>
                                                    <small class="text-muted">Frecuencia de backup automático de datos</small>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Retención de Datos</label>
                                                    <select class="form-select" id="selectRetencionDatos">
                                                        <option value="3">3 meses</option>
                                                        <option value="6">6 meses</option>
                                                        <option value="12" selected>12 meses</option>
                                                        <option value="24">24 meses</option>
                                                        <option value="forever">Para siempre</option>
                                                    </select>
                                                    <small class="text-muted">Período de retención de datos históricos</small>
                                                </div>
                                                
                                                <div class="mb-3">
                                                    <label class="form-label">Tamaño Máximo Backup</label>
                                                    <div class="input-group">
                                                        <input type="number" class="form-control" id="tamanioMaximoBackup" value="100" min="10" max="1000">
                                                        <span class="input-group-text">MB</span>
                                                    </div>
                                                    <small class="text-muted">Tamaño máximo permitido para backups</small>
                                                </div>
                                                
                                                <div class="d-grid gap-2">
                                                    <button class="btn btn-success" onclick="crearBackupManual()">
                                                        <i class="fas fa-save me-2"></i>Crear Backup Manual
                                                    </button>
                                                    <button class="btn btn-info" onclick="restaurarBackup()">
                                                        <i class="fas fa-undo me-2"></i>Restaurar desde Backup
                                                    </button>
                                                    <button class="btn btn-warning" onclick="limpiarDatosTemporales()">
                                                        <i class="fas fa-broom me-2"></i>Limpiar Datos Temporales
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                
                                <div class="row mt-3">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-sync-alt me-2"></i>Sincronización de Catálogos
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="form-check">
                                                            <input class="form-check-input" type="checkbox" id="checkSincCentros" checked>
                                                            <label class="form-check-label" for="checkSincCentros">
                                                                Sincronizar Centros de Costo
                                                            </label>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="form-check">
                                                            <input class="form-check-input" type="checkbox" id="checkSincElementos" checked>
                                                            <label class="form-check-label" for="checkSincElementos">
                                                                Sincronizar Elementos de Costo
                                                            </label>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="form-check">
                                                            <input class="form-check-input" type="checkbox" id="checkSincProveedores" checked>
                                                            <label class="form-check-label" for="checkSincProveedores">
                                                                Sincronizar Proveedores
                                                            </label>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-2">
                                                    <div class="col-md-4">
                                                        <div class="form-check">
                                                            <input class="form-check-input" type="checkbox" id="checkSincInsumos">
                                                            <label class="form-check-label" for="checkSincInsumos">
                                                                Sincronizar Insumos
                                                            </label>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="form-check">
                                                            <input class="form-check-input" type="checkbox" id="checkSincActivos">
                                                            <label class="form-check-label" for="checkSincActivos">
                                                                Sincronizar Activos
                                                            </label>
                                                        </div>
                                                    </div>
                                                    <div class="col-md-4">
                                                        <div class="form-check">
                                                            <input class="form-check-input" type="checkbox" id="checkSincConfiguracion" checked>
                                                            <label class="form-check-label" for="checkSincConfiguracion">
                                                                Sincronizar Configuración
                                                            </label>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="mt-3">
                                                    <button class="btn btn-configuracion" onclick="sincronizarCatalogos()">
                                                        <i class="fas fa-sync-alt me-2"></i>Sincronizar Catálogos Seleccionados
                                                    </button>
                                                    <button class="btn btn-outline-secondary ms-2" onclick="verEstadoSincronizacion()">
                                                        <i class="fas fa-info-circle me-2"></i>Ver Estado de Sincronización
                                                    </button>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Período -->
                            <div class="tab-pane fade" id="config-periodo">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-calendar-alt me-2"></i>Gestión de Período Contable
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Apertura de Período</h6>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Mes y Año</label>
                                                                    <div class="row">
                                                                        <div class="col-md-6">
                                                                            <select class="form-select" id="selectMesApertura">
                                                                                <option value="1">Enero</option>
                                                                                <option value="2">Febrero</option>
                                                                                <option value="3">Marzo</option>
                                                                                <option value="4">Abril</option>
                                                                                <option value="5">Mayo</option>
                                                                                <option value="6">Junio</option>
                                                                                <option value="7">Julio</option>
                                                                                <option value="8">Agosto</option>
                                                                                <option value="9">Septiembre</option>
                                                                                <option value="10">Octubre</option>
                                                                                <option value="11">Noviembre</option>
                                                                                <option value="12">Diciembre</option>
                                                                            </select>
                                                                        </div>
                                                                        <div class="col-md-6">
                                                                            <input type="number" class="form-control" id="inputAnioApertura" value="2026" min="2024" max="2030">
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Tasa BCV Vigente</label>
                                                                    <div class="input-group">
                                                                        <input type="number" class="form-control" id="tasaBCVApertura" value="36.00" step="0.0001" min="0">
                                                                        <span class="input-group-text">Bs/$</span>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Estado Inicial</label>
                                                                    <select class="form-select" id="selectEstadoInicial">
                                                                        <option value="abierto">Abierto</option>
                                                                        <option value="pendiente">Pendiente</option>
                                                                    </select>
                                                                </div>
                                                                
                                                                <div class="d-grid">
                                                                    <button class="btn btn-success" id="btnAperturarPeriodoConfig" onclick="aperturarPeriodoConfig()">
                                                                        <i class="fas fa-folder-open me-2"></i>Aperturar Período
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Cierre de Período</h6>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Período Actual</label>
                                                                    <div class="p-2 border rounded bg-light">
                                                                        <strong id="periodoActualConfig">--/----</strong>
                                                                        <div class="small">Estado: <span id="estadoPeriodoActual" class="badge periodo-abierto">Abierto</span></div>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Responsable Cierre</label>
                                                                    <input type="text" class="form-control" id="responsableCierre" placeholder="Nombre del responsable">
                                                                </div>
                                                                
                                                                <div class="mb-3">
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkGenerarReporteCierre" checked>
                                                                        <label class="form-check-label" for="checkGenerarReporteCierre">
                                                                            Generar reporte consolidado
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkFirmaDigitalCierre" checked>
                                                                        <label class="form-check-label" for="checkFirmaDigitalCierre">
                                                                            Aplicar firma digital
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkBloquearEdicion">
                                                                        <label class="form-check-label" for="checkBloquearEdicion">
                                                                            Bloquear edición (solo lectura)
                                                                        </label>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="d-grid">
                                                                    <button class="btn btn-danger" id="btnCerrarPeriodoConfig" onclick="cerrarPeriodoConfig()" disabled>
                                                                        <i class="fas fa-lock me-2"></i>Cerrar Período
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Calendario Fiscal y Reversión Controlada</h6>
                                                                
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Año Fiscal</label>
                                                                            <input type="number" class="form-control" id="anioFiscal" value="2026" min="2024" max="2030">
                                                                        </div>
                                                                        
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Mes Inicio Año Fiscal</label>
                                                                            <select class="form-select" id="mesInicioFiscal">
                                                                                <option value="1">Enero</option>
                                                                                <option value="4">Abril</option>
                                                                                <option value="7">Julio</option>
                                                                                <option value="10">Octubre</option>
                                                                            </select>
                                                                        </div>
                                                                    </div>
                                                                    
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Períodos Cerrados</label>
                                                                            <div class="p-2 border rounded bg-light" style="max-height: 100px; overflow-y: auto;">
                                                                                <div id="listaPeriodosCerrados">No hay períodos cerrados</div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="row mt-3">
                                                                    <div class="col-md-12">
                                                                        <div class="alert alert-warning">
                                                                            <i class="fas fa-exclamation-triangle me-2"></i>
                                                                            <strong>Reversión Controlada:</strong> La reversión de períodos cerrados solo está disponible para usuarios administradores y requiere autorización.
                                                                            <button class="btn btn-sm btn-outline-warning ms-2" onclick="mostrarModalReversion()">
                                                                                <i class="fas fa-undo me-1"></i>Solicitar Reversión
                                                                            </button>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Roles -->
                            <div class="tab-pane fade" id="config-roles">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-user-shield me-2"></i>Roles y Permisos
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-user-cog fa-3x text-primary mb-3"></i>
                                                                <h6>Administrador</h6>
                                                                <p class="small">Acceso completo a todos los módulos y configuraciones.</p>
                                                                <div class="metric-value" id="totalAdministradores">1</div>
                                                                <div class="metric-unit">Usuarios</div>
                                                                <button class="btn btn-sm btn-outline-primary mt-2" onclick="gestionarAdministradores()">
                                                                    <i class="fas fa-cog me-1"></i>Gestionar
                                                                </button>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-user-edit fa-3x text-success mb-3"></i>
                                                                <h6>Operador</h6>
                                                                <p class="small">Puede registrar datos pero no modificar configuraciones.</p>
                                                                <div class="metric-value" id="totalOperadores">0</div>
                                                                <div class="metric-unit">Usuarios</div>
                                                                <button class="btn btn-sm btn-outline-success mt-2" onclick="gestionarOperadores()">
                                                                    <i class="fas fa-cog me-1"></i>Gestionar
                                                                </button>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-4">
                                                        <div class="card mb-3">
                                                            <div class="card-body text-center">
                                                                <i class="fas fa-user-check fa-3x text-info mb-3"></i>
                                                                <h6>Auditor</h6>
                                                                <p class="small">Solo lectura, puede ver reportes pero no modificar datos.</p>
                                                                <div class="metric-value" id="totalAuditores">0</div>
                                                                <div class="metric-unit">Usuarios</div>
                                                                <button class="btn btn-sm btn-outline-info mt-2" onclick="gestionarAuditores()">
                                                                    <i class="fas fa-cog me-1"></i>Gestionar
                                                                </button>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Permisos por Módulo</h6>
                                                                <div class="table-responsive">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Módulo</th>
                                                                                <th>Administrador</th>
                                                                                <th>Operador</th>
                                                                                <th>Auditor</th>
                                                                                <th>Gerencia</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaPermisos">
                                                                            <tr>
                                                                                <td>Producción</td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-eye text-info"></i></td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Servicios</td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-eye text-info"></i></td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Impuestos</td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-eye text-info"></i></td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Reportes</td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-eye text-info"></i></td>
                                                                                <td><i class="fas fa-eye text-info"></i></td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Configuración</td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-times text-danger"></i></td>
                                                                                <td><i class="fas fa-times text-danger"></i></td>
                                                                                <td><i class="fas fa-eye text-info"></i></td>
                                                                            </tr>
                                                                            <tr>
                                                                                <td>Cierre Período</td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                                <td><i class="fas fa-times text-danger"></i></td>
                                                                                <td><i class="fas fa-times text-danger"></i></td>
                                                                                <td><i class="fas fa-check text-success"></i></td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Gestión de Usuarios</h6>
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <button class="btn btn-primary" onclick="mostrarModalNuevoUsuario()">
                                                                            <i class="fas fa-user-plus me-2"></i>Nuevo Usuario
                                                                        </button>
                                                                        <button class="btn btn-outline-secondary ms-2" onclick="exportarListaUsuarios()">
                                                                            <i class="fas fa-download me-2"></i>Exportar Lista
                                                                        </button>
                                                                    </div>
                                                                    <div class="col-md-6">
                                                                        <div class="search-box">
                                                                            <i class="fas fa-search search-icon"></i>
                                                                            <input type="text" id="searchUsuarios" class="form-control" placeholder="Buscar usuarios...">
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="table-responsive mt-3">
                                                                    <table class="table table-sm">
                                                                        <thead>
                                                                            <tr>
                                                                                <th>Usuario</th>
                                                                                <th>Nombre</th>
                                                                                <th>Rol</th>
                                                                                <th>Email</th>
                                                                                <th>Estado</th>
                                                                                <th>Último Acceso</th>
                                                                                <th>Acciones</th>
                                                                            </tr>
                                                                        </thead>
                                                                        <tbody id="tablaUsuarios">
                                                                            <tr>
                                                                                <td>admin</td>
                                                                                <td>Administrador Sistema</td>
                                                                                <td><span class="badge bg-primary">Administrador</span></td>
                                                                                <td>admin@vencement.com</td>
                                                                                <td><span class="badge bg-success">Activo</span></td>
                                                                                <td>Hoy 10:30</td>
                                                                                <td>
                                                                                    <button class="btn btn-sm btn-outline-primary">
                                                                                        <i class="fas fa-edit"></i>
                                                                                    </button>
                                                                                </td>
                                                                            </tr>
                                                                        </tbody>
                                                                    </table>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Subpestaña Auditoría -->
                            <div class="tab-pane fade" id="config-auditoria">
                                <div class="row">
                                    <div class="col-md-12">
                                        <div class="card">
                                            <div class="card-header configuracion">
                                                <i class="fas fa-clipboard-check me-2"></i>Auditoría y Trazabilidad
                                            </div>
                                            <div class="card-body">
                                                <div class="row">
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Logs de Cambios</h6>
                                                                <p class="text-muted">Registro detallado de todos los cambios en el sistema.</p>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Nivel de Log</label>
                                                                    <select class="form-select" id="selectNivelLog">
                                                                        <option value="minimo">Mínimo (solo cambios críticos)</option>
                                                                        <option value="normal" selected>Normal (cambios importantes)</option>
                                                                        <option value="detallado">Detallado (todos los cambios)</option>
                                                                        <option value="debug">Debug (información completa)</option>
                                                                    </select>
                                                                </div>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Retención de Logs</label>
                                                                    <select class="form-select" id="selectRetencionLogs">
                                                                        <option value="30">30 días</option>
                                                                        <option value="90">90 días</option>
                                                                        <option value="180" selected>180 días</option>
                                                                        <option value="365">1 año</option>
                                                                        <option value="forever">Para siempre</option>
                                                                    </select>
                                                                </div>
                                                                
                                                                <div class="form-check mb-3">
                                                                    <input class="form-check-input" type="checkbox" id="checkLogUsuarios" checked>
                                                                    <label class="form-check-label" for="checkLogUsuarios">
                                                                        Registrar usuario en cada cambio
                                                                    </label>
                                                                </div>
                                                                
                                                                <div class="form-check mb-3">
                                                                    <input class="form-check-input" type="checkbox" id="checkLogIP">
                                                                    <label class="form-check-label" for="checkLogIP">
                                                                        Registrar dirección IP
                                                                    </label>
                                                                </div>
                                                                
                                                                <div class="form-check mb-3">
                                                                    <input class="form-check-input" type="checkbox" id="checkLogTimestamp" checked>
                                                                    <label class="form-check-label" for="checkLogTimestamp">
                                                                        Registrar timestamp preciso
                                                                    </label>
                                                                </div>
                                                                
                                                                <div class="d-grid">
                                                                    <button class="btn btn-configuracion" onclick="guardarConfiguracionLogs()">
                                                                        <i class="fas fa-save me-2"></i>Guardar Configuración Logs
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    
                                                    <div class="col-md-6">
                                                        <div class="card mb-3">
                                                            <div class="card-body">
                                                                <h6>Versionado de Parámetros</h6>
                                                                <p class="text-muted">Control de versiones para configuraciones importantes.</p>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Parámetros con Versionado</label>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkVersionTasas" checked>
                                                                        <label class="form-check-label" for="checkVersionTasas">
                                                                            Tasas de cambio
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkVersionRegalias" checked>
                                                                        <label class="form-check-label" for="checkVersionRegalias">
                                                                            Regalías e impuestos
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkVersionConfig" checked>
                                                                        <label class="form-check-label" for="checkVersionConfig">
                                                                            Configuración general
                                                                        </label>
                                                                    </div>
                                                                    <div class="form-check">
                                                                        <input class="form-check-input" type="checkbox" id="checkVersionCatalogos">
                                                                        <label class="form-check-label" for="checkVersionCatalogos">
                                                                            Catálogos del sistema
                                                                        </label>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="mb-3">
                                                                    <label class="form-label">Máximo de Versiones Guardadas</label>
                                                                    <input type="number" class="form-control" id="maxVersionesGuardadas" value="10" min="1" max="50">
                                                                </div>
                                                                
                                                                <div class="d-grid gap-2">
                                                                    <button class="btn btn-info" onclick="verHistorialVersiones()">
                                                                        <i class="fas fa-history me-2"></i>Ver Historial de Versiones
                                                                    </button>
                                                                    <button class="btn btn-warning" onclick="restaurarVersionAnterior()">
                                                                        <i class="fas fa-undo me-2"></i>Restaurar Versión Anterior
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                
                                                <div class="row mt-3">
                                                    <div class="col-md-12">
                                                        <div class="card">
                                                            <div class="card-body">
                                                                <h6>Firmas Digitales y Hash</h6>
                                                                
                                                                <div class="row">
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Algoritmo de Hash</label>
                                                                            <select class="form-select" id="selectAlgoritmoHash">
                                                                                <option value="sha256">SHA-256</option>
                                                                                <option value="sha512">SHA-512</option>
                                                                                <option value="md5">MD5</option>
                                                                            </select>
                                                                        </div>
                                                                        
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Clave de Firma</label>
                                                                            <div class="input-group">
                                                                                <input type="password" class="form-control" id="claveFirma" value="VENCEMENT2026">
                                                                                <button class="btn btn-outline-secondary" type="button" onclick="toggleClaveFirma()">
                                                                                    <i class="fas fa-eye"></i>
                                                                                </button>
                                                                            </div>
                                                                            <small class="text-muted">Clave para generar firmas digitales</small>
                                                                        </div>
                                                                    </div>
                                                                    
                                                                    <div class="col-md-6">
                                                                        <div class="mb-3">
                                                                            <label class="form-label">Documentos con Firma Digital</label>
                                                                            <div class="form-check">
                                                                                <input class="form-check-input" type="checkbox" id="checkFirmaReportes" checked>
                                                                                <label class="form-check-label" for="checkFirmaReportes">
                                                                                    Reportes consolidados
                                                                                </label>
                                                                            </div>
                                                                            <div class="form-check">
                                                                                <input class="form-check-input" type="checkbox" id="checkFirmaCierres" checked>
                                                                                <label class="form-check-label" for="checkFirmaCierres">
                                                                                    Cierres de período
                                                                                </label>
                                                                            </div>
                                                                            <div class="form-check">
                                                                                <input class="form-check-input" type="checkbox" id="checkFirmaAuditoria">
                                                                                <label class="form-check-label" for="checkFirmaAuditoria">
                                                                                    Reportes de auditoría
                                                                                </label>
                                                                            </div>
                                                                            <div class="form-check">
                                                                                <input class="form-check-input" type="checkbox" id="checkFirmaExportaciones">
                                                                                <label class="form-check-label" for="checkFirmaExportaciones">
                                                                                    Exportaciones masivas
                                                                                </label>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="row mt-3">
                                                                    <div class="col-md-12">
                                                                        <div class="card">
                                                                            <div class="card-body">
                                                                                <h6>Verificación de Integridad</h6>
                                                                                <div class="row">
                                                                                    <div class="col-md-6">
                                                                                        <div class="metric-value" id="hashSistemaActual">-</div>
                                                                                        <div class="metric-unit">Hash del sistema actual</div>
                                                                                    </div>
                                                                                    <div class="col-md-6">
                                                                                        <div class="metric-value" id="fechaUltimaVerificacion">-</div>
                                                                                        <div class="metric-unit">Última verificación</div>
                                                                                    </div>
                                                                                </div>
                                                                                <div class="mt-3">
                                                                                    <button class="btn btn-success" onclick="verificarIntegridadSistema()">
                                                                                        <i class="fas fa-shield-alt me-2"></i>Verificar Integridad del Sistema
                                                                                    </button>
                                                                                    <button class="btn btn-outline-secondary ms-2" onclick="generarHashActual()">
                                                                                        <i class="fas fa-fingerprint me-2"></i>Generar Hash Actual
                                                                                    </button>
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                
                                                                <div class="row mt-3">
                                                                    <div class="col-md-12">
                                                                        <div class="export-buttons">
                                                                            <button class="btn btn-primary" onclick="exportarLogsAuditoriaCompleto()">
                                                                                <i class="fas fa-download me-2"></i>Exportar Logs de Auditoría
                                                                            </button>
                                                                            <button class="btn btn-info" onclick="
