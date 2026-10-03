# Contrato DTO (Data Transfer Objects)

Este documento congela la estructura de los objetos que viajan a través de los 15 endpoints definidos en el contrato de API.

## 1. ProductDTO (Salida)
- id (string/UUID)
- 
ame (string)
- price (string, decimal representation)
- stock (int)
- category (string)
- image_url (string, nullable)

## 2. SaleDTO (Salida)
- id (string/UUID)
- seller_name (string)
- 	otal (string, decimal)
- created_at (string, ISO8601)
- lines (Array of SaleLineDTO)

## 3. SaleLineDTO (Salida)
- product_id (string/UUID)
- product_name (string, snapshot congelado)
- unit_price (string, decimal, snapshot congelado)
- quantity (int)
- subtotal (string, decimal)

*(Este contrato es inmutable para la capa Presentation)*
