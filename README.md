# 🚗 A.D.A.M. — Asistente de Diagnóstico Automotriz Mecánico

[![Último Release](https://img.shields.io/github/v/release/MidKnight458/ADAM?label=Release&color=blue)](https://github.com/MidKnight458/ADAM/releases/latest)
[![Plataforma](https://img.shields.io/badge/Plataforma-Windows-0078D6?logo=windows&logoColor=white)](https://github.com/MidKnight458/ADAM/releases/latest)
[![Base de Conocimiento](https://img.shields.io/badge/Base%20de%20Conocimiento-152%20Reglas%20%7C%2015%20M%C3%B3dulos-2CC985)](#cobertura-de-diagnóstico)
[![Tecnologías](https://img.shields.io/badge/Stack-Python%203.10%2B%20%7C%20CustomTkinter%20%7C%20SQL%20Server-informational)](#compilar-y-ejecutar-desde-el-código-fuente)

**A.D.A.M.** (*Asistente de Diagnóstico Automotriz Mecánico*) es un sistema experto de diagnóstico automotriz basado en reglas que guía al usuario mediante preguntas sencillas y lectura de códigos OBD-II para identificar posibles fallas mecánicas, eléctricas y de sensores en su vehículo.

---

### Índice rápido

- [¿Qué es A.D.A.M.? y características principales](#qué-es-adam-y-características-principales)
- [Cobertura de diagnóstico (15 módulos · 152 reglas)](#cobertura-de-diagnóstico)
- [Descarga (Releases)](#-descarga-releases)
- [Cómo usar A.D.A.M.](#-cómo-usar-adam)
- [Compilar y ejecutar desde el código fuente](#-compilar-y-ejecutar-desde-el-código-fuente)
- [Estructura del proyecto](#-estructura-del-proyecto)
- [Aviso de seguridad automotriz](#-aviso-de-seguridad-automotriz)
- [Autor](#-autor)

---

## ¿Qué es A.D.A.M.? y características principales

A.D.A.M. combina una base de conocimiento automotriz de **152 reglas** con un motor de inferencia encadenada para ayudar tanto a conductores como a técnicos a acotar fallas comunes y críticas del automóvil de forma estructurada:

- **Diagnóstico Básico (Guiado paso a paso):** recorre la base de conocimiento completa haciendo preguntas directas de **SÍ / NO** (y captura de códigos DTC cuando aplica), ideal si no tienes conocimientos mecánicos previos o aún no identificas el origen de la falla.
- **Diagnóstico Avanzado (Por Módulo):** permite seleccionar directamente el sistema del vehículo afectado (frenos, enfriamiento, A/C, transmisión, códigos DTC, etc.) desde una cuadrícula visual para ir directo al área de interés.
- **Lectura de códigos OBD-II (DTCs):** interpreta códigos estándar frecuentes como `P0300`, `P030X`, `P0420`, `P0171`, `P0172`, `P0401`, `P0404`, `P0442`, `P0455`, `P0443` y `P0456`, ofreciendo causas probables y comprobaciones sugeridas.
- **Motor de inferencia con base de datos SQL Server:** las reglas, condiciones y consecuencias se cargan dinámicamente desde la base de datos `ADAM_DB` (`Reglas`, `Condiciones`, `Consecuencias`), lo que permite actualizar o ampliar el conocimiento sin recompilar la aplicación.
- **Interfaz moderna y herramientas adicionales:**
  - Aplicación de escritorio en modo oscuro con `CustomTkinter` (`adam_gui.py` / `adam_gui.exe`).
  - Interfaz de línea de comandos conectada a SQL Server (`adam_cli.py`).
  - Motor de inferencia autónomo de simulación local sin SQL Server (`motor_inferencia.py`).
  - Visualizador interactivo de red semántica en HTML (`red_adam.html`).

---

## Cobertura de diagnóstico

La base de conocimiento de A.D.A.M. abarca **152 reglas** organizadas en **15 módulos**:

| # | Módulo | Fallas y síntomas que analiza |
| :-: | :--- | :--- |
| 1 | **Sistema de Enfriamiento** | Sobrecalentamiento del motor, fugas externas e internas, termostato atascado, radiador de calefacción (*heater core*), junta de culata y fallas del motoventilador. |
| 2 | **Sistema de Combustible** | Motor que gira pero no arranca, nivel de combustible, activación de la bomba de gasolina, filtro obstruido, pérdida de potencia bajo carga e inyectores. |
| 3 | **Sistema de Encendido** | Ralentí inestable, desgaste de bujías, cables o bobinas dañadas, válvula IAC, luz *Check Engine* fija o parpadeante, tapón de gasolina y sensores CKP, CMP, MAF y O2. |
| 4 | **Problemas Mecánicos Mayores** | Alerta crítica de correa de distribución rota (motor se apaga en marcha con sonido de arranque anormalmente rápido). |
| 5 | **Sistema de Lubricación (Aceite)** | Testigo de presión de aceite, golpeteo metálico (*knocking*), humo azulado, fugas de aceite, contaminación lechosa con anticongelante y ruido de taquetes. |
| 6 | **Sistema de Frenos** | Indicadores de desgaste en pastillas, roce metálico (*grinding*), pedal esponjoso o muy duro, vibración de discos alabeados, desviación al frenar, ABS y servofreno (*booster*). |
| 7 | **Sistema Eléctrico (Batería y Alternador)** | Batería descargada o débil, corrosión en terminales, fallas de carga del alternador y pérdida de intensidad de luces en ralentí. |
| 8 | **Suspensión, Dirección y Neumáticos** | Golpeteos en baches (bieletas, bujes, rótulas), amortiguadores desgastados, desbalanceo, alineación, baleros de rueda, junta homocinética y dirección hidráulica. |
| 9 | **Sistema de Escape** | Fugas en silenciador o tubería, catalizador suelto u obstruido y presencia peligrosa de gases de escape en la cabina. |
| 10 | **Transmisión (Automática y Manual)** | Golpes o cambios bruscos en transmisión automática, patinamiento, falla hidráulica del clutch y desgaste del embrague en transmisión manual. |
| 11 | **Sensores Avanzados** | Diagnóstico profundo de sensores **ECT** (temperatura de refrigerante), **OPS** (presión de aceite) y **TPS** (posición del acelerador). |
| 12 | **Códigos de Falla (DTCs / OBD-II)** | Análisis guiado para `P0300` (misfire aleatorio), `P030X` (cilindro específico), `P0420` (eficiencia del catalizador), `P0171` (mezcla pobre) y `P0172` (mezcla rica). |
| 13 | **Sistema de Aire Acondicionado (A/C)** | Compresor sin activación o ciclos cortos, baja carga o fugas de refrigerante, obstrucciones, filtro de cabina, compuerta de mezcla (*blend door*), ruidos y soplador. |
| 14 | **Sistema de Emisiones (EGR y EVAP)** | Válvula EGR atascada abierta/cerrada (`P0401`, `P0404`), fugas EVAP (`P0442`, `P0455`, `P0456`), válvula de purga (`P0443`), saturación del cánister y fallas en verificación. |
| 15 | **Carrocería y Eléctricos Menores** | Luces exteriores/interiores, fusibles y cortocircuitos, ventanas y seguros eléctricos, ruidos de viento y filtraciones de agua por drenajes obstruidos. |

---

## 📦 Descarga (Releases)

Puedes descargar la versión compilada lista para usar en Windows desde la página de Releases del repositorio:

- 👉 **[Descargar última versión (`v1.0.0`)](https://github.com/MidKnight458/ADAM/releases/latest)**
- 📋 **[Ver todas las versiones en Releases](https://github.com/MidKnight458/ADAM/releases)**

Descarga el archivo **`adam_gui.exe`** (ejecutable autónomo de Windows, no requiere instalar Python).

> [!NOTE]
> **Aviso sobre Windows SmartScreen:** Al ser un ejecutable empaquetado sin certificado comercial de firma de código, Windows Defender SmartScreen puede mostrar una advertencia preventiva al abrirlo por primera vez. Haz clic en **"Más información"** y luego en **"Ejecutar de todas formas"**.

### Requisitos del entorno para ejecutar `adam_gui.exe`

El ejecutable carga las reglas dinámicamente desde SQL Server al iniciar, por lo que tu equipo Windows (64 bits) debe contar con:

1. **Microsoft SQL Server** activo en la instancia local predeterminada (`.`) con autenticación integrada de Windows (`Trusted_Connection=yes`).
2. **[Microsoft ODBC Driver 17 for SQL Server](https://learn.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server)** instalado.
3. La base de datos **`ADAM_DB`** creada y poblada (consulta el paso [Crear y poblar la base de datos `ADAM_DB`](#3-crear-y-poblar-la-base-de-datos-adam_db) más abajo).

---

## 🧭 Cómo usar A.D.A.M.

### Aplicación de escritorio (`adam_gui.exe` o `adam_gui.py`)

1. **Verifica la conexión:** asegúrate de que el servicio de SQL Server esté iniciado y abre `adam_gui.exe`. En la parte inferior de la pantalla principal deberás ver el mensaje:
   `Conectado: 152 reglas cargadas.`
   *(Si aparece un error SQL en rojo, revisa los requisitos de instancia y driver ODBC en la sección anterior).*
2. **Elige un modo de operación:**
   - **Diagnóstico Básico:** responde **SÍ** o **NO** a las preguntas mostradas en pantalla. Cuando el asistente pregunte por un código de falla OBD-II, haz clic en **Ingresar Código** y escribe el código leído por tu escáner (por ejemplo: `P0300`, `P0420`, `P0171`).
   - **Diagnóstico Avanzado:** selecciona el módulo específico del vehículo en la cuadrícula de botones y responde únicamente las preguntas correspondientes a esa área.
3. **Consulta el resultado:** al concluir la inferencia se desplegará el **Diagnóstico Final** con las causas probables y acciones recomendadas. Puedes usar **Nuevo Diagnóstico** o `< Menú` para realizar otra consulta.

### Explorar la Red Semántica (`red_adam.html`)

Si deseas visualizar el mapa completo de relaciones entre módulos, síntomas y diagnósticos sin necesidad de configurar SQL Server ni Python, abre el archivo [`red_adam.html`](red_adam.html) directamente en cualquier navegador web moderno para navegar, hacer zoom y arrastrar los nodos del grafo interactivo.

---

## 🛠️ Compilar y ejecutar desde el código fuente

### Requisitos previos

- **Python 3.10 o superior** (desarrollado y probado con Python 3.14).
- **Microsoft SQL Server** y **ODBC Driver 17 for SQL Server**.
- **Git** para clonar el repositorio.

### 1. Clonar el repositorio

```bash
git clone https://github.com/MidKnight458/ADAM.git
cd ADAM
```

### 2. Crear entorno virtual e instalar dependencias

```bash
python -m venv .venv
.venv\Scripts\activate
pip install customtkinter pyodbc
```

Dependencias opcionales según lo que necesites ejecutar o compilar:

```bash
# Opcional: para regenerar el grafo interactivo (red.py)
pip install networkx pyvis

# Opcional: para compilar el ejecutable (.exe) con PyInstaller
pip install pyinstaller
```

### 3. Crear y poblar la base de datos `ADAM_DB`

1. Abre **SQL Server Management Studio (SSMS)** (o `sqlcmd`) y ejecuta el script para crear `ADAM_DB` y sus tres tablas (`Reglas`, `Condiciones`, `Consecuencias`).
2. Revisa la constante `CONNECTION_STRING` en los scripts antes de ejecutar:
   - En [`adam_gui.py`](adam_gui.py#L21-L26) apunta por defecto a `SERVER=.;` (instancia local predeterminada). Cámbialo si usas una instancia con nombre (por ejemplo, `LOCALHOST\SQLEXPRESS`) antes de ejecutar o compilar.
   - En [`migrar_a_sql.py`](migrar_a_sql.py#L6-L11) y [`adam_cli.py`](adam_cli.py#L183-L188) apunta a `SERVER=MIDKNIGHT;`. **Sustituye `MIDKNIGHT` por `.`, `LOCALHOST\SQLEXPRESS` o el nombre de tu servidor SQL.**
3. Ejecuta el script de migración para insertar las 152 reglas desde `base_conocimiento.py`:
   ```bash
   python migrar_a_sql.py
   ```
4. Ejecuta el script de asignación de módulos (`UPDATE Reglas SET Modulo = ...`) incluido en el desplegable para habilitar la agrupación por módulos en el modo **Diagnóstico Avanzado** (de lo contrario todas aparecerán bajo `"General"`).

<details>
<summary>Ver script SQL completo para crear ADAM_DB y asignar módulos</summary>

```sql
CREATE DATABASE ADAM_DB;
GO

USE ADAM_DB;
GO

CREATE TABLE Reglas (
    ID_Regla INT IDENTITY(1,1) PRIMARY KEY,
    Descripcion NVARCHAR(255) NOT NULL,
    Modulo NVARCHAR(100) NULL
);

CREATE TABLE Condiciones (
    ID_Condicion INT IDENTITY(1,1) PRIMARY KEY,
    ID_Regla INT NOT NULL FOREIGN KEY REFERENCES Reglas(ID_Regla),
    Variable NVARCHAR(100) NOT NULL,
    Valor NVARCHAR(255) NOT NULL,
    Operador_Siguiente NVARCHAR(10) NULL,
    Orden INT NOT NULL
);

CREATE TABLE Consecuencias (
    ID_Consecuencia INT IDENTITY(1,1) PRIMARY KEY,
    ID_Regla INT NOT NULL FOREIGN KEY REFERENCES Reglas(ID_Regla),
    Variable NVARCHAR(100) NOT NULL,
    Valor NVARCHAR(MAX) NOT NULL
);
GO
```

Después de ejecutar `python migrar_a_sql.py`, ejecuta este bloque en `ADAM_DB` para clasificar las 152 reglas en sus módulos correspondientes según el orden de inserción en `base_conocimiento.py`:

```sql
USE ADAM_DB;
GO

WITH ReglasNumeradas AS (
    SELECT
        ID_Regla,
        TRY_CAST(REPLACE(Descripcion, 'Regla ', '') AS INT) AS Num
    FROM Reglas
)
UPDATE r
SET r.Modulo = CASE
    WHEN rn.Num BETWEEN 1 AND 17 THEN N'Sistema de Enfriamiento'
    WHEN rn.Num BETWEEN 18 AND 26 THEN N'Sistema de Combustible'
    WHEN rn.Num BETWEEN 27 AND 39 THEN N'Sistema de Encendido'
    WHEN rn.Num BETWEEN 40 AND 41 THEN N'Mecánica Mayor'
    WHEN rn.Num BETWEEN 42 AND 47 THEN N'Sistema de Lubricación'
    WHEN rn.Num BETWEEN 48 AND 54 THEN N'Sistema de Frenos'
    WHEN rn.Num BETWEEN 55 AND 61 THEN N'Sistema Eléctrico'
    WHEN rn.Num BETWEEN 62 AND 69 THEN N'Suspensión y Dirección'
    WHEN rn.Num BETWEEN 70 AND 73 THEN N'Sistema de Escape'
    WHEN rn.Num BETWEEN 74 AND 77 THEN N'Transmisión'
    WHEN rn.Num BETWEEN 78 AND 90 THEN N'Sensores Avanzados'
    WHEN rn.Num BETWEEN 91 AND 105 THEN N'Códigos de Falla (DTC)'
    WHEN rn.Num BETWEEN 106 AND 120 THEN N'Aire Acondicionado'
    WHEN rn.Num BETWEEN 121 AND 135 THEN N'Emisiones (EGR/EVAP)'
    WHEN rn.Num BETWEEN 136 AND 148 THEN N'Eléctricos Menores'
    WHEN rn.Num BETWEEN 149 AND 152 THEN N'Carrocería'
    ELSE N'General'
END
FROM Reglas r
INNER JOIN ReglasNumeradas rn ON r.ID_Regla = rn.ID_Regla;
GO
```

</details>

### 4. Ejecutar desde Python

```bash
# Interfaz gráfica de escritorio (CustomTkinter + SQL Server)
python adam_gui.py

# Interfaz de consola interactiva (SQL Server)
python adam_cli.py

# Prueba del motor de inferencia sin SQL Server (casos simulados en memoria)
python motor_inferencia.py

# Regenerar la red semántica interactiva (genera y abre red_adam.html)
python red.py
```

### 5. Compilar el ejecutable `.exe` con PyInstaller

Para generar tu propio ejecutable independiente para Windows:

**Opción A — Usando el archivo `.spec` del proyecto (recomendado):**

```bash
pyinstaller adam_gui.spec
```

**Opción B — Compilando directamente desde cero:**

```bash
pyinstaller --onefile --windowed --collect-all customtkinter --name adam_gui adam_gui.py
```

Al finalizar, encontrarás el binario compilado en `dist/adam_gui.exe`.

---

## 📁 Estructura del proyecto

| Archivo / Carpeta | Descripción |
| :--- | :--- |
| [`adam_gui.py`](adam_gui.py) | Aplicación de escritorio principal en `CustomTkinter` con Diagnóstico Básico y Avanzado por módulos. |
| [`adam_cli.py`](adam_cli.py) | Versión en consola del motor de diagnóstico conectada a SQL Server (`ADAM_DB`). |
| [`base_conocimiento.py`](base_conocimiento.py) | Base de conocimiento completa con las 152 reglas estructuradas (`si` / `entonces`). |
| [`motor_inferencia.py`](motor_inferencia.py) | Motor de inferencia autónomo en Python para pruebas y simulaciones sin base de datos. |
| [`migrar_a_sql.py`](migrar_a_sql.py) | Script de migración para cargar las 152 reglas de `base_conocimiento.py` hacia SQL Server. |
| [`red.py`](red.py) | Generador de la red semántica (`NetworkX` + `PyVis`) que exporta el grafo a HTML. |
| [`red_adam.html`](red_adam.html) | Visualización web interactiva pre-generada de módulos, síntomas y diagnósticos. |
| [`adam_gui.spec`](adam_gui.spec) | Archivo de especificación de PyInstaller para empaquetar `adam_gui.py` con `customtkinter`. |
| [`dist/adam_gui.exe`](dist/adam_gui.exe) | Ejecutable precompilado para Windows (también disponible en Releases). |

---

## ⚠️ Aviso de seguridad automotriz

> [!WARNING]
> A.D.A.M. es una herramienta de apoyo orientativo y educativo basada en reglas diagnósticas. **No sustituye la inspección física ni el criterio de un técnico mecánico certificado.** Ante advertencias críticas —como testigo de presión de aceite encendido, pérdida de frenos, sospecha de correa de distribución rota o presencia de gases de escape en la cabina— detén el vehículo de forma segura y solicita asistencia mecánica profesional inmediata.

---

## 👤 Autor

Desarrollado por **[MidKnight458](https://github.com/MidKnight458)**.
