Consignas:

1. Escriba el código de SQL que le permite conocer el monto y la cantidad de las transacciones que SIMETRIK considera como conciliables para la base de CLAP

código de SQL:

select count(*) as cantidad_conc, sum(MONTO) as monto_conciliable from bansur_2 where TIPO_TRX = 'PAGO';

2. Escriba el código de SQL que le permite conocer el monto y la cantidad de las transacciones que SIMETRIK considera como conciliables para la base de BANSUR

código de SQL:

select count(*) as cantidad_conc, sum(MONTO) as monto_conciliable  from clap_2  where TIPO_TRX = 'PAGADA';

3. ¿Cómo se comparan las cifras de los puntos anteriores respecto de las cifras totales en las fuentes desde un punto de vista del negocio?

Las cifras totales de la base de CLAP y BANCUR contienen otro tipo de transacciones a considerar ademas de las transacciones concialibles, como por ejemplo las de cancelaciones, entre otras.
Esas cifras repercuten el monto total ya que al haber transacciones de cancelacion el monto es negativo.

4. Teniendo en cuenta los criterios de cruce entre ambas bases conciliables, escriba una sentencia de SQL que contenga la información de CLAP y BANSUR; agregue una columna en la que se evidencie si la transacción cruzó o no con su contrapartida y una columna en la que se inserte un ID autoincremental para el control de la conciliación


DECLARE @row_number INT;
SET @row_number = 0;
SELECT ROW_NUMBER() OVER (ORDER BY (SELECT NULL)) AS row_number, 
		CASE 
			WHEN c.ID_BANCO is null or b.ID_ADQUIRIENTE is null THEN 'NO'
			ELSE 'SI'
		END AS cruzo_contrapartida,
		b.*,
		c.*
from bansur_2 b  
full join clap_2 c 
	ON (b.ID_ADQUIRIENTE = c.ID_BANCO and 
		b.CODIGO_AUTORIZACION  = c.CODIGO_AUTORIZACION and 
		SUBSTRING(b.TARJETA, 1, 6) = c.INICIO6_TARJETA and 
		SUBSTRING(b.TARJETA, 7, 10) = c.FINAL4_TARJETA and 
		c.FECHA_TRANSACCION = b.FECHA_TRANSACCION);


5. Diseñe un código que calcule el porcentaje de transacciones de la base conciliable de CLAP cruzó contra la liquidación de BANSUR.

6. Diseñe un código que calcule el porcentaje de transacciones de la base conciliable de BANSUR no cruzó contra la liquidación de CLAP.
