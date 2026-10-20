# Decisiones para publicar en decisiones.md (piezas 0, 1 y 2)

Formato de una línea por decisión. Pegar cada bloque en la sección de quien lo publica.

## Publicación 1 — Clasificación (domingo 21:00, la consume la Fase 2 y el QAW)

- D-01 · R5 y R15 son requerimientos de PROCESO (no RF ni RNF, no RAS) · R2 es la restricción ergonómica de hardware (RNF, RAS por Det Tec/usabilidad)
- D-02 · RNF = R2, R11, R13 · RF = R1, R3, R4, R6, R7, R8, R9, R10, R12, R14 · 11 RAS: R1, R2, R3, R4, R6, R7, R10, R11, R12, R13, R14 · no RAS: R5, R8, R9, R15
- D-03 · Atributos Bass/SEI: rendimiento (R4, R6, R7, R12), escalabilidad (R13, R7), disponibilidad (R11), seguridad (R3, R10, R14), interoperabilidad (R12, R14), usabilidad (R2), modificabilidad (R1)
- D-04 · Candidatos a QAW: rendimiento (R4/R6, eventos Last Gasp hasta el mapa), escalabilidad (R13, 800.000 → 2.000.000 medidores), disponibilidad (R11, caída de un nodo sin perder datagramas)

## Publicación 2 — Dorfman Fase 1 (domingo 21:00, la consume el CUC de R4 y R7)

- D-05 · Los 10 RF se descomponen en 35 RF atómicos (R1.1, R1.2, …): 11 macro y 24 sub; 8 son implícitos (derivados de R15 y del texto)
- D-06 · 7 dominios: D1 Ingesta y Telemetría AMI, D2 Gestión de Eventos y Alarmas, D3 Operación de Campo, D4 Monitoreo Georreferenciado, D5 Analítica de Balance y Pérdidas, D6 Administración y Seguridad, D7 Servicios Abiertos (APIs)
- D-07 · Casos de uso base de R4 y R7: R4.1 Visualizar mapa georreferenciado (include: R4.2 estado, R4.3 tiempo real; extend: R9.1 zonas asignadas) y R7.1 Estimar balance mensual (include: R7.2, R7.3, R7.4, R7.5, R7.6)
- D-08 · Ciclo de vida del evento: registrado → notificado → en atención → normalizado (R1.3–R1.5); sesión del operador: iniciada → activa → cerrada (R10.3)

## Publicación 3 — Lista de componentes (lunes 14:00, la consume el deployment)

- D-09 · 8 subsistemas: S1 Ingesta y Mensajería AMI, S2 Procesamiento de Eventos y Alarmas, S3 Almacenamiento y Consulta de Telemetría, S4 Monitoreo Georreferenciado, S5 Analítica de Balance y Pérdidas, S6 Administración y Seguridad, S7 Servicios Abiertos (APIs), S8 Terminal de Campo
- D-10 · S1: C01 ReceptorDatagramasAMI (recibe del head-end), C02 ParserDatagramaAMI (R12), C03 BusMensajeriaTelemetria (desacopla, absorbe picos)
- D-11 · S2: C04 ClasificadorEventosRed, C05 GestorCicloVidaEventos, C06 NotificadorOperadores, C07 CatalogoEventos · S3: C08 AlmacenSeriesTiempo (particionado y replicado), C09 ServicioConsultaTelemetria
- D-12 · S4: C10 ServicioMapaRed, C11 ActualizadorTiempoReal (WSS), C12 GestorVistaOperador, C13 CatalogoTopologiaRed (PostgreSQL + PostGIS), C14 ConsolaWebCOD · S5: C15 OrquestadorAnaliticaPerdidas, C16 CalculadorBalanceTransformador (MIMD), C17 AgregadorBalanceCircuito
- D-13 · S6: C18 GestorUsuariosRoles, C19 AutenticadorSesiones, C20 AutorizadorAcceso, C21 GestorAsignaciones · S7: C22 GatewayAPIServicios, C23 CalculadorIndicesCalidad · S8: C24 AplicacionTerminalCampo, C25 ControladorBotonesTerminal
- D-14 · Protocolos sugeridos para el deployment: MQTT/TLS desde head-end, Kafka/TLS entre componentes, gRPC interno, HTTPS/REST + WSS hacia navegador y APIs, base de series de tiempo (TCP 5432), JDBC a PostgreSQL/PostGIS

## Juan — decisiones (literal A)

- D-J01 · CUC en src/JuanDiegoBalantaMolina_ValeriaPiza_AlejandroRendon_A_CUC.vpp (PDF en PDF/). Límite del sistema: «Plataforma de Telemetría y Análisis de la Red Eléctrica» (igual que la hoja Dorfman F2); paquetes = dominios D1, D2·D3, D4, D5, D6 de la Fase 1 · lunes 22:15
- D-J02 · Actores humanos: Operador del COD, Analista de pérdidas, Administrador del sistema · Actores dispositivo con estereotipo «dispositivo» (naranja): Smart Meter, Macromedidor, Terminal de Campo · lunes 22:15
- D-J03 · 20 casos de uso, cada uno con el ID de su RF atómico: CU-01 (R4.1) incluye CU-02 (R4.2) y CU-03 (R4.3); CU-04 (R9.1) extiende CU-01 [operador con asignación vigente] e incluye CU-05 (R9.2); CU-06 (R7.1) incluye CU-07..CU-11 (R7.6, R7.2, R7.3, R7.4, R7.5); CU-02, CU-08 y CU-09 incluyen CU-15 (R6.3) · lunes 22:15
- D-J04 · Ingesta y eventos como "demás directamente implicados": CU-12 (R6.1) incluye CU-13 (R12.1) y CU-14 (R6.2); CU-16 (R1.1, R1.2) extiende CU-12 [código de evento ≠ normal]; CU-17 (R1.7) incluye CU-18 (R1.8); además CU-19 Iniciar sesión (R10.1) y CU-21 Asignar circuitos y zonas (R8.1) · lunes 22:15
- D-J05 · R3.4 (autorizar por rol) NO se dibuja como caso de uso: queda como precondición en la bicolumnar para no mezclar detalle de implementación en el CUC · lunes 22:15
- D-J06 · La Terminal de Campo es actor dispositivo externo; la app C24 de Valeria es el artefacto que Alejandro despliega en ese nodo · lunes 22:15
- D-J07 · R15: dos diagramas de estados en el mismo .vpp. Evento: (inicio) → Registrado → Notificado → En atención → Normalizado → (fin), más Notificado → Normalizado por restablecimiento automático. Sesión: (inicio) → Iniciada → Activa → Cerrada → (fin), con cierre por cerrarSesion() o por inactividad. Componentes que los implementan: C04/C05/C06 y C19/C20/C12 · lunes 23:55
- D-J08 · Bicolumnar en src/…_A_Bicolumnar_y_Estados.docx (formato del informe de Valeria, continúa la numeración: Parte IV, Parte V, Tabla 9 en adelante, Figura 2 en adelante). Se especifican CU-01 (principal, R4) y CU-06 (primario de R7). % pérdidas no técnicas = (inyectada − consumida) / inyectada × 100 · lunes 23:55
- D-J09 · Trazabilidad (parte de Juan): en reques.xlsx se agregó la columna L «ID en el CUC (literal A)» en «Dorfman F1» (35/35 RF mapeados) y la columna H «Literal A: CUC y estados (R15)» en «Cobertura R1-R15». Falta la parte de Alejandro (nodo y escenario QAW) · martes 17:10
- D-J10 · El límite del sistema en el CUC se renombró a «Plataforma de Telemetría y Análisis de la Red Eléctrica», igual que la hoja «Dorfman F2»; Word y PDF regenerados · martes 17:10

## Hallazgos de revisión

Revisión de Juan (con IA) sobre las piezas 0, 1, 2 y B de Valeria, contra la rúbrica. El dueño decide qué corrige.

- H-01 · Criterio 2 · Media · C10 ServicioMapaRed calcula el estado «sospecha de fraude», pero en su tarjeta CRC no colabora con la analítica (C15/C16/C17). Sugerencia: agregar IBalanceCircuito o ICalculoBalanceTransformador como interfaz requerida de C10 (así cuadra con el paso 3 de la bicolumnar de CU-01, donde el fraude sale del % de pérdidas de CU-06).
- H-02 · Criterio 1 · Decidir · La rúbrica pide clasificar en Sistema/Proceso/Producto; el informe usa Naturaleza (Proceso/Producto) más los pilares Hw/Red/Sw. Sugerencia: una frase en Parte I que diga explícitamente cuáles son «de Sistema» (p. ej. los que involucran hardware, redes y software a la vez: R1, R11, R13) o que la columna de pilares es esa dimensión.
- H-03 · Criterio 1 · Baja · R9 queda como no RAS. Con 30 operadores concurrentes en tiempo real podría leerse como RAS de rendimiento; basta reforzar en la justificación por qué no condiciona la arquitectura (lo cubre R4).
- H-04 · Empaquetado · Alta · El informe cita el anexo como JuanDiegoBalantaMolina_ValeriaPiza_AlejandroRendon_0_Clasificacion_Dorfman.xlsx, pero el archivo se llama reques.xlsx y está en la raíz; informe.docx tampoco tiene el prefijo ni está en src/. Renombrar y mover antes del .zip, y exportar ambos a PDF.
- H-05 · Forma · Baja · En el Excel actualizado las filas 1–2 de cada hoja quedaron vacías (se quitaron los títulos). Cosmético.
- Verificado sin problemas: 35 RF = 11 macro + 24 sub (19 obligatorios, 5 condicionales), 8 implícitos; partición a tercer nivel (1 sistema, 8 subsistemas, 25 componentes); 25 interfaces provistas y 53 requeridas, todas consistentes entre tarjetas CRC y hoja «Interfaces y Protocolos»; cobertura R1–R15 sin huecos.
