Consignas:

1. Escriba el código de SQL que le permite conocer el monto y la cantidad de las transacciones que SIMETRIK considera como conciliables para la base de CLAP

select count(*) as cantidad_conc, sum(MONTO) as monto_conciliable from bansur_2 where TIPO_TRX = 'PAGO';

2. Escriba el código de SQL que le permite conocer el monto y la cantidad de las transacciones que SIMETRIK considera como conciliables para la base de BANSUR

´´´select count(*) as cantidad_conc, sum(MONTO) as monto_conciliable  from clap_2  where TIPO_TRX = 'PAGADA';´´´

3. ¿Cómo se comparan las cifras de los puntos anteriores respecto de las cifras totales en las fuentes desde un punto de vista del negocio?

4. Teniendo en cuenta los criterios de cruce entre ambas bases conciliables, escriba una sentencia de SQL que contenga la información de CLAP y BANSUR; agregue una columna en la que se evidencie si la transacción cruzó o no con su contrapartida y una columna en la que se inserte un ID autoincremental para el control de la conciliación

5. Diseñe un código que calcule el porcentaje de transacciones de la base conciliable de CLAP cruzó contra la liquidación de BANSUR.

6. Diseñe un código que calcule el porcentaje de transacciones de la base conciliable de BANSUR no cruzó contra la liquidación de CLAP.
