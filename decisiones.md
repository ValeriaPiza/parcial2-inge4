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
