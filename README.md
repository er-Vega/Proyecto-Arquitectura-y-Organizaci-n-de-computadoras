# Arquitectura y Organización de computadoras
<h1 align="center"><img src="https://www.msx.org/sites/default/files/news/2024/04/goodbyez80.jpg" width="250"> </h1>

## Repositorio de recursos utilizados para la simulación del proyecto 

Para evaluar el funcionamiento del circuito antes de su montaje físico, se utilizó el software SimulIDE, el cual permite simular componentes electrónicos en tiempo real. Con esta herramienta fue posible verificar el comportamiento del diseño, identificar posibles errores en la implementación. 
[Descargar SimulIDE:](https://www.google.com)

### *El siguiente repositorio contiene :* 

#### - **Archivo de la simulación en SimulIDE:**
  - El archivo se encuentra en el repositorio con el nombre
~~~
SIMULADOR_Z80CONTRASEÑA.sim1 
~~~
#### - **Video de la simulación en funcionamiento:**

<a href="https://youtu.be/5_olUpJl4kw">
  <img src="https://img.shields.io/badge/YouTube-%23FF0000.svg?style=for-the-badge&logo=YouTube&logoColor=white" alt="Youtube">
</a>

#### - **Código compilado .hex**
  - El archivo se encuentra en el repositorio con el nombre:
~~~
programaCONTRASEÑA.hex 
~~~
  - El contenido del compilado es:
~~~
:100000002100017E473200202100E07E32012021C4
:1000100001017E3202203A0120B80EFF20063E0187
:09002000ED7918043E02ED797639
:00000001FF
~~~
##### - **Código fuente de ensamblador Z80 utilizado para el proyecto:**
~~~
ORG 0000h

    ; Leer datos directamente a registros
    LD HL, 0100h      ; Dirección ROM 0100h
    LD A, (HL)        ; Leer primer dato
    LD B, A           ; Guardar en B para comparación posterior
    LD (2000h), A     ; Guardar copia en RAM 2000h

    ; Leer segundo dato de E000h
    LD HL, 0E000h     ; Dirección E000h
    LD A, (HL)        ; Leer segundo dato
    LD (2001h), A     ; Guardar en RAM 2001h

    ; Leer tercer dato de 0101h
    LD HL, 0101h      ; Dirección ROM 0101h
    LD A, (HL)        ; Leer tercer dato
    LD (2002h), A     ; Guardar en RAM 2002h

    ; Comparar B (primer dato) con A (segundo dato)
    LD A, (2001h)     ; Recargar segundo dato
    CP B              ; Comparar con primer dato (en B)

    ; Preparar puerto
    LD C, 0FFh        ; Puerto FFh en C

    JR NZ, diferentes ; Saltar si NO son iguales

    ; Son iguales: enviar 01b
    LD A, 00000001b   ; D0=1, D1=0
    OUT (C), A
    JR fin

diferentes:
    LD A, 00000010b   ; D0=0, D1=1
    OUT (C), A

fin:
    HALT
~~~
<!--  -->

