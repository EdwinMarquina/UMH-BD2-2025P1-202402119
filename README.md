DELIMITER //
DROP PROCEDURE sp_new_currency_case;
 
DELIMITER //
CREATE procedure sp_new_currency_case(
in p_currency_name varchar(45), 
in P_currency_symbol varchar (45), 
in p_exchange_rate decimal (15, 2),
in p_country varchar(45), 
in p_iso_code varchar(45)
)
BEGIN 
/*Declaracion oe varzabzes*/

DECLARE v_currency_name varchar(45) default null;
DECLARE v_currency_symbol varchar (45);
DECLARE v_exchange_rate decimal(15,2);
DECLARE v_country varchar(45);


set v_currency_name = p_currency_name;
set v_currency_symbol = p_currency_symbol;
set v_exchange_rate = P_exchange_rate;
set v_country = p_country;
set v_iso_code = p_iso_code;
/*case statement */

CASE
WHEN p_currency_name LiKE '%dolar%' THEN Set v_currency_symbol = "$";
WHEN p_currency_name LIKE '%peso%' THEN Set v_currency_symbol = "P";
WHEN p_currency_name LIKE '%yen%' THEN Set v_currency_symbol = "y";
WHEN p_currency_name LIKE '%euro%' THEN Set v_currency_symbol = "€";

ELSE
set v_currency_symbol = p_currency_symbol;
END CASE;
INSERT INTO currencies ( currency_name, currency_symbol, exchange_rate, country, ISO_CODE)
VALUES (v_currency_name, _currency_symbol, v_exchange_rate, v_country, v_iso_code) ;
commit;
END;

CALl db_demo.sp_new_currency_case(
"sol peruano",0,"PERU" 
);

select * from db_demo.currencies WHERE currency_name LIKE '%euro%'
