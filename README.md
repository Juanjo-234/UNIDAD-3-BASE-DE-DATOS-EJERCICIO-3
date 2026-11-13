# UNIDAD-3-BASE-DE-DATOS-EJERCICIO-3
El diagrama muestra un **Modelo Relacional (MR)** orientado a la gestión de un centro médico o clínica, compuesto por 6 tablas interconectadas que administran la información de pacientes, turnos, médicos, especialidades y recetas de medicamentos.

A continuación, se detalla la estructura y las relaciones de cada tabla:

---

### 1. Tablas y Estructura

* **PACIENTE**
* `NUMERO_HISTORIAL_CLINICA` (PK)


* `DNI`


* `NOMBRE`


* `OBRA_SOCIAL`


* `DOMICILIO`




* **TURNO**
* `NUMERO_TURNO` (PK)


* `FECHA`


* `HORA`


* `ESTADO`


* `DIAGNOSTICO`




* **MEDICO**
* `NUMERO_MATRICULA` (PK)


* `NOMBRE`


* `TELEFONO`




* **MEDICO_ESPECIALIDAD** (Tabla intermedia / asociativa entre Médico y Especialidad)
* `NUMERO_MATRICULA` (PK / FK)


* `ID_ESPECIALIDAD` (PK / FK)


* `NOMBRE_ESPECIALIDAD`


* `TIPO_ESPECIALIDAD`




* **ESPECIALIDAD**
* `ID_ESPECIALIDAD` (PK)


* `NOMBRE`




* **RECETA** (Tabla intermedia / asociativa entre Turno y Medicamento)
* `NUMERO_TURNO` (PK / FK)


* `CODIGO_ALFANUMERICO` (PK / FK)


* `DOSIS`


* `FRECUENCIA`


* `DURACION`




* **MEDICAMENTO**
* `CODIGO_ALFANUMERICO` (PK)


* `MONODROGA`


* `FABRICANTE`


* `NOMBRE_COMERCIAL`





---

### 2. Relaciones Principales

* **Paciente y Turno:** Un paciente puede solicitar y registrar múltiples turnos médicos a lo largo del tiempo, mientras que un turno específico pertenece a un único paciente (relación de uno a muchos).


* **Médico y Turno:** Un médico atiende múltiples turnos, y un turno es asignado a un único médico (relación de uno a muchos).


* **Médico y Especialidad:** Existe una relación de muchos a muchos resuelta por la tabla `MEDICO_ESPECIALIDAD`, lo que permite que un médico posea múltiples especialidades y que una especialidad sea ejercida por varios médicos.


* **Turno y Medicamento (Receta):** La tabla `RECETA` actúa como una entidad asociativa de muchos a muchos entre el turno médico y los medicamentos. Permite prescribir múltiples fármacos en una consulta, detallando las pautas de administración como la dosis, la frecuencia y la duración del tratamiento.
<img width="1882" height="632" alt="EJERCICIO 3-MR drawio" src="https://github.com/user-attachments/assets/4faff448-92c3-4739-80c0-f098b3a55be1" />

La imagen muestra el proceso completo de **normalización de bases de datos** aplicado de manera secuencial —desde una tabla inicial desnormalizada hasta alcanzar la Tercera Forma Normal (3NF)— para un sistema de gestión de clínica médica (turnos, pacientes, médicos, especialidades y recetas de medicamentos).

A continuación, se detalla lo que se realiza en cada fase representada en el esquema:

---

### 1. Fase de Normalización N°0 (Tabla Desnormalizada)

* **Estado inicial:** Se parte de una **única tabla grande y plana** que agrupa todos los datos mezclados y redundantes (número de turno, fecha, hora, estado, diagnóstico, datos del paciente, datos del médico, especialidad y los detalles farmacológicos de las recetas).
* **Problema:** Presenta una fuerte redundancia y repetición de datos, lo que provoca anomalías de inserción, actualización y borrado en el sistema.

### 2. Primera Forma Normal (1NF)

* **Condición:** Se asegura que todos los atributos contengan valores atómicos y que cada tabla cuente con una clave primaria identificativa.
* **Proceso aplicado:** Se desglosa la información para aislar las entidades independientes:
* **TABLA PACIENTE:** Extrae los datos personales y de historia clínica de los pacientes utilizando `NUMERO_HISTORIAL_CLINICA` como Clave Primaria (PK).
* **TABLA MEDICO:** Agrupa la información de los profesionales de la salud con `NUMERO_MATRICULA` como PK.



### 3. Segunda Forma Normal (2NF)

* **Condición:** La base de datos debe estar en 1NF y **todos los atributos que no forman parte de la clave deben depender por completo de toda la clave primaria** (eliminando dependencias parciales).
* **Proceso aplicado:** Se reestructuran las tablas operativas y de relación:
* **TABLA TURNO:** Contiene los datos principales de cada consulta médica vinculando al paciente y al médico mediante claves foráneas.
* **TABLA RECETA:** Funciona como una tabla intermedia o de detalle relacionada con el turno, extrayendo las pautas de prescripción y la dosis de los medicamentos.
* **TABLA MEDICAMENTO:** Aísla el catálogo farmacológico mediante su código alfanumérico.



### 4. Tercera Forma Normal (3NF)

* **Condición:** Debe estar en 2NF y **carecer de dependencias transitivas** (ningún atributo no clave debe depender de otro atributo que tampoco sea clave; todo debe depender estrictamente de la clave primaria).
* **Proceso aplicado:** Se estructuran de forma definitiva e independiente todas las entidades del sistema clínico:
* **TABLA MEDICAMENTO:** Almacena de forma limpia los fármacos, monodrogas y fabricantes.
* **TABLA ESPECIALIDAD:** Contiene el registro de las especialidades médicas.
* **TABLA MEDICO_ESPECIALIDAD:** Resuelve la relación de muchos a muchos entre los médicos y sus respectivas especialidades.
* **TABLA MEDICO y TABLA PACIENTE:** Mantienen de manera independiente la información de las personas.
* **TABLA TURNO:** Gestiona las citas médicas con sus diagnósticos y estados.
* **TABLA RECETA:** Registra con precisión los medicamentos recetados por turno (dosis, frecuencia y duración).
<img width="4852" height="2665" alt="EJERCICIO 3-FASES DE NORMALIZACION drawio" src="https://github.com/user-attachments/assets/1ffac938-4878-403e-ba05-dd8a102639d7" />
