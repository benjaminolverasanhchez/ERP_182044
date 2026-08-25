```mermaid
```mermaid
flowchart LR
    %% Estilos de nodos y estados
    classDef stepNode fill:#FFFFFF,stroke:#00A88F,stroke-width:2px,rx:12,ry:12,color:#000000,font-size:12px;
    classDef openStatus fill:#DDF6FD,stroke:#3BAFD8,stroke-width:2px,color:#000000,font-size:11px;
    classDef closedStatus fill:#D7F3D0,stroke:#5BAA4F,stroke-width:2px,color:#000000,font-size:11px;

    %% ----------------------------------------------------
    %% ORDEN DE VENTA BASE
    %% ----------------------------------------------------
    SO["🛒<br/><b>Sales Order</b><br/>Total Qty: 10"]:::stepNode

    %% ----------------------------------------------------
    %% ENTREGAS PARCIALES
    %% ----------------------------------------------------
    D1["🚚<br/><b>Partial Delivery 1</b><br/>Qty: 6"]:::stepNode
    ST_OPEN["<b>Sales Order Status:</b><br/>Status: Open<br/>Open Qty: 4"]:::openStatus

    D2["🚚<br/><b>Partial Delivery 2</b><br/>Qty: 4"]:::stepNode
    ST_CLOSED["<b>Sales Order Status:</b><br/>Status: Closed<br/>Open Qty: 0"]:::closedStatus

    %% ----------------------------------------------------
    %% FACTURACIÓN Y PAGO
    %% ----------------------------------------------------
    INV["📄<br/><b>A/R Invoice</b><br/>Total Invoiced: 10"]:::stepNode
    PAY["💵<br/><b>Incoming Payment</b>"]:::stepNode

    %% Conexiones del flujo
    SO -->|Copy to (Parcial 1)| D1
    D1 -.->|Actualiza estado| ST_OPEN
    
    ST_OPEN -->|Copy to (Parcial 2)| D2
    D2 -.->|Actualiza estado| ST_CLOSED

    D1 -->|Factura entrega 1| INV
    D2 -->|Factura entrega 2| INV
    INV --> PAY
```
