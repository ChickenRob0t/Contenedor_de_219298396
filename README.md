\documentclass[12pt,a4paper]{report}

% Packages
\usepackage{graphicx}
\usepackage{amsmath}
\usepackage{hyperref}
\usepackage{setspace}
\usepackage{xcolor}

\usepackage{background}


% Title and Author (adjust the spacing as needed)
\title{\LARGE \textbf{PROJECT TITLE}}
\author{}
\date{\large On: \today}

% Begin Document
\begin{document}

\backgroundsetup{
scale=1,
angle=0,
opacity=1,  %% adjust
contents={\includegraphics[width=\paperwidth,height=\paperheight ]{Averr.png}}
}


% Title Page
\makeatletter
\begin{titlepage}
    \centering
    \vspace*{1cm}
       { \includegraphics[width=8cm]{images.png}}\\[2cm]

    {\LARGE \textbf{
    Llenado de base REPUVE Tonalá}}\\[5cm]

    
    Consejo Estatal de Seguridad Pública \hspace{3}
    Área: Informática
    
    Luis Ramón Mendoza Escareño\\[1.5cm]


    
   
\end{titlepage}
\makeatother

% Table of Contents
\tableofcontents


% Resumen
\chapter*{Resumen}
\addcontentsline{toc}{chapter}{Resumen}
Se realiza un trabajo en conjunto con el módulo de Tonalá para obtener una base de datos homologada y completa, esto a partir de la inserción de documentos con los que no se contaban (Archivo de texto de la ANAM, constancia y Acuse firmado por el beneficiario), este proceso se generó en alrededor de 10,000 casos.

% Chapters
\chapter*{Introducción}
\addcontentsline{toc}{chapter}{Introducción}
El módulo de regularización de Tonalá lleva regularizando vehículos desde octubre del 2022, sin embargo no fue hasta \textbf{Abril} del 2024 %no estoy seguro de esto xdd 
que se informó que dentro de esta compilación de archivos se debía incluír los archivos de información que provee la plataforma ANAM, además de la constancia y el acuse firmado por el benefactor. \\

Esta tarea se abordó en dos partes, el módulo de Tonalá dedicándose a homologar el nombre de los archivos, inspeccionar los documentos y añadir el archivo que provee la plataforma ANAM, mientras que en nuestra área escaneamos los archivos de acuse y Constancia para agregarlos en su carpeta correspondiente.\\


\section{Planteamiento del problema}
Debido a diversas situaciones estas carpetas no están estructuradas de un modo conveniente para este problema. Entre las dificultades que se tienen para realizarlo, las más relevantes son:

\begin{itemize}
    \item Las carpetas de cada auto regularizado tienen un nombre con el siguiente formato: ''# de ficha, nombre de la persona, últimos 4 números del NIV, comentario'', acomodo el cual no siempre se respeta.
    \item Los archivos físicos están acomodados por un \textbf{Folio}, información la cual no se encuentra en las carpetas y por tanto como paso intermedio se tiene que buscar en una base de datos que contenga ambos.
    \item En la base de datos de apoyo y las carpetas las fechas de cada regularizado no suele coincidir.
    \item Debido a que sólo se utilizan los 4 últimos números del NIV, suele coincidir con más de un NIV de la base de datos.
    \item Por errores de escritura aveces los números de las carpetas no coinciden con los de la base.
\end{itemize}

Por todos estos aspectos, además de no tener escaneados los aproximadamente 10,000 documentos hacen que esta tarea se vuelva tediosa y larga.

\chapter*{Metodología}
\addcontentsline{toc}{chapter}{Metodología}
La manera en que se pasan los documentos a sus respectivas carpetas fue evolucionando: \\
Al principio era completamente manual e ineficiente, acomodando aproximadamante 1 caso cada 4 minutos.\\

La segunda forma fue a partir de código el cual buscaba en la base de datos que coincidieran los 4 números de al final, estos se enlistaban, se buscan físicamente, escanean y automáticamente se parte el PDF en cada NIV para colocarse en su respectiva carpeta, el cual en promedio nos permitió reducir el tiempo a una cuarta parte (aproximadamente 1 minuto por caso).\\
El último y más eficiente método consta de los siguientes pasos:
\section{Escaneados de PDF general y extracción de información}
Se escanean muchos documentos consecutivos con un escáner de alta calidad. A partir de este escaneo se extrae información relevante de cada caso, cosas como el nombre, NIV, fecha y folio a partir del método OCR.

\section{Corte y partición de los PDFS}
Teniendo la información relevante del documento, el NIV se busca en la base de datos con el criterio de búsqueda de Levenshtein y si este coincide en un $90\%$ se guarda el NIV como correcto para al final cortar el PDF completo en muchos de estos con su respectivo NIV como nombre.\\

En el siguiente paso de la base de datos se extrae el nombre del registrado, si este coincide en un $80\%$ a partir de la métrica de Levenshtein con el nombre de la carpeta y los 4 últimos dígitos del NIV esta se toma como la carpeta correspondiente al documento.\\

Los casos que no coincidan o que no cumplan con este método se buscan manualmente hasta encontrar su carpeta o en su defecto estar seguro que no tiene asignada una carpeta.\\

Finalmente ya con cada carpeta asignada a cada documento por medio de una función se corta el PDF en 2 partes la del acuse y la constancia documentos los cuales se traspasan directamente a su carpeta correspondiente.\\

\section{Monitoreo}
Finalmente se aplica una 'auditoría', la cual de cada carpeta que se tiene identifica la cantidad y el tipo de archivos que se tienen a partir de los nombres que tienen. De esta forma se pueden analizar e identificar las falta de documentos en las regularizaciones.

\section{Herramientas para la gestión del proyecto}
\textbf{Tecnologías}\\
\begin{itemize}
    \item Python (De manera local con jupyter notebook)\\
\end{itemize}


\textbf{Dependencias}\\
\begin{itemize}
    \item time (gestión del tiempo en el código)
    \item pandas (Manejo de bases de datos)
    \item PyPDF2 (Manejo de PDF y extracción de texto)
    \item pathlib,os, shutil (Acceso y manejo de carpetas para guardar los documentos)
    \item re   (Filtrado de expresiones regulares)
    \item Levenshtein (Métrica para ver el parecido de dos cadenas de texto)
    \item matplotlib.pyplot (Herramienta para graficar resultados)
\end{itemize}



\chapter*{Resultados}
\addcontentsline{toc}{chapter}{Resultados}
Por nuestra parte está completo el trabajo, ya que se han pasado todos los documentos de los casos hacia sus respectivas carpetas, las cuales se entregan al módulo de Tonalá para que se revisen y se agreguen los documentos TXT. Hasta ahora se tiene una base de datos de Tonalá desde 2022 hasta JULIO de 2023 la cual sigue en actualización por parte del módulo.


\section{Evaluación de resultados}
Se tiene ya la base de datos hasta Julio de 2023, además se tiene ya el código necesario para evualuar con la auditoría qué tipo de archivos faltan, de qué meses, cuántos no se regularizaron entre otras aplicaciones. Sólo se necesitan los documentos por parte de Tonalá.
%Aquí podría poner una comparación de los autos con el DRIVE, la ANAM, y ambas bases de datos o algo así :P, además de generar un porcentaje de documentos 
\section{Trabajos próximos/relacionados}

\subsection{Análisis de datos}
Al ya tener los archivos ordenados y homologados, se pueden extraer y hacer un resumen de las bases de datos con información como:\\
Cantidad de autos regularizados, cantidad de autos que no fueron regularizados, casos en los que les faltan documentos, meses con más o menos regularizados, entre otras cosas.

\subsection{Acceso rápido a archivos fundamentales}
Debido a que ahora se tiene una base estructurada y bien descrita, se pueden hacer interfaces gráficas para acceder a ciertos documentos de forma sencilla.\\
\textcolor{blue}{Código y documentación -- Interfaz\_Deteccion/... }

\subsection{Chequeo de documentos}
Existen algunos documentos cruciales en los cuales se pueden identificar errores, ahora debido a que están estandarizados, es posible acceder a estos documentos, encontrar las partes cruciales y determinar así si concuerdan los datos o no, esto con el fin de darle un seguimiento o determinar por qué fue así.\\
\textcolor{blue}{Código y documentación -- Interfaz\_Deteccion/... }

\subsection{Extracción de información automática}
Es posible utilizando otras herramientas como el OCR de muchos de estos documentos extraer la información y estructurarla en bases de datos para una mayor facilidad de análisis el contenido de estos documentos.\\
\textcolor{blue}{Documentación, Código y bases de datos -- Estructuración\_PDF/...}


\end{document}
