# SMART_LIFE_KNOWAGE

## EXTERNAL SOURCES
meteodata and sensors: https://dash.iotsens.sk/
vehicles counting: https://vms.canex.sk/api/task_result_interval/4611686018784950001/900/2022-12-12T23:00:00/2022-12-13T23:00:00

## MARIA DB - connection and creating smart_life database
download MARIADB 10.9

login: mysql -u root -padmin

from maria db command prompt run zipped mariaDB_dump.sql

## KNOWAGE data source
url: jdbc:mariadb://localhost:3306/smart_life?user=root&password=admin

driver: org.mariadb.jdbc.Driver

user: root
password: admin

## KNOWAGE dataset (created by query) - about 1390 rows (with aliases) - data from all sensors, ordered by sensor ids and date_time for 24 hours rounded to 15 minutes intervals
SELECT a.id as 'SENSOR_ID', b.place as 'PLACE', b.gps as 'GPS', AVG(a.bmp_t) as 'TEMPERATURE', AVG(a.sht_t) as 'SHT_T', AVG(a.mc_pm_1_0) as 'MC_PM_1', AVG(a.mc_pm_2_5) as 'MC_PM_2_5', AVG(a.mc_pm_4_0) as 'MC_PM_4', AVG(a.mc_pm_10) as 'MC_PM_10', AVG(a.nc_pm_0_5) as 'NC_PM_0_5', AVG(a.nc_pm_1_0) as 'NC_PM_1', AVG(a.nc_pm_2_5) as 'NC_PM_2_5', AVG(a.nc_pm_4_0) as 'NC_PM_4', AVG(a.nc_pm_10) 'NC_PM_10', AVG(a.type_particle_size) as 'PART_SIZE', AVG(a.si_lux) as 'LUX', AVG(a.si_uv) as 'UV', AVG(a.sht_hygro) as 'HYGRO', AVG(a.bmp_press) as 'PRESSURE', DATE_FORMAT(FROM_UNIXTIME(ROUND(a.timestamp/900)*900),'%D %b %H:%i') as 'DATE_TIME', AVG(a.v_bat) as 'BAT', AVG(a.energy) as 'ENERGY', AVG(a.v_in) as 'IN', AVG(a.msg_c) as 'MSG', AVG(a.pms_pm_1_0) as 'PMS_PM_1', AVG(a.pms_pm_2_5) as 'PMS_PM_2_5', AVG(a.pms_10) as 'PMS_PM_10', AVG(a.pms_env_1) as 'PMS_ENV_1', AVG(a.pms_env_2_5) as 'PMS_ENV_2_5', AVG(a.pms_env_10_0) as 'PMS_ENV_10', AVG(a.pms_env_0_3_c) as 'PMS_ENV_0_3_C', AVG(a.pms_env_0_5_c) as 'PMS_ENV_0_5_C', AVG(a.pms_env_1_0_c) as 'PMS_ENV_1_0_C', AVG(a.pms_env_2_5_c)  as 'PMS_ENV_2_5_C', AVG(a.pms_env_5_0_c) as 'PMS_ENV_5_0_C', AVG(a.pms_env_10_0_c)  as 'PMS_ENV_10_0_C', a.systick as 'SYSTICK', AVG(a.rssi) as 'RSSI' from measures a inner join sensors b on b.id_sensor = a.id where a.timestamp between 1663941491 and 1664027891 group by a.id, DATE_FORMAT(FROM_UNIXTIME(ROUND(a.timestamp/900)*900),'%D %b %H:%i') order by FROM_UNIXTIME(a.timestamp) asc;

## if we have small number of sensors, we can create dataset for each sensor ordered by date_time for 24 hours rounded to 15 minutes intervals from altrenative dataset - about 250 - 286 rows (with aliases)
SELECT a.id as 'SENSOR_ID', b.place as 'PLACE', b.gps as 'GPS', AVG(a.bmp_t) as 'TEMPERATURE', AVG(a.sht_t) as 'SHT_T', AVG(a.mc_pm_1_0) as 'MC_PM_1', AVG(a.mc_pm_2_5) as 'MC_PM_2_5', AVG(a.mc_pm_4_0) as 'MC_PM_4', AVG(a.mc_pm_10) as 'MC_PM_10', AVG(a.nc_pm_0_5) as 'NC_PM_0_5', AVG(a.nc_pm_1_0) as 'NC_PM_1', AVG(a.nc_pm_2_5) as 'NC_PM_2_5', AVG(a.nc_pm_4_0) as 'NC_PM_4', AVG(a.nc_pm_10) 'NC_PM_10', AVG(a.type_particle_size) as 'PART_SIZE', AVG(a.si_lux) as 'LUX', AVG(a.si_uv) as 'UV', AVG(a.sht_hygro) as 'HYGRO', AVG(a.bmp_press) as 'PRESSURE', DATE_FORMAT(FROM_UNIXTIME(ROUND(a.timestamp/900)*900),'%D %b %H:%i') as 'DATE_TIME', AVG(a.v_bat) as 'BAT', AVG(a.energy) as 'ENERGY', AVG(a.v_in) as 'IN', AVG(a.msg_c) as 'MSG', AVG(a.pms_pm_1_0) as 'PMS_PM_1', AVG(a.pms_pm_2_5) as 'PMS_PM_2_5', AVG(a.pms_10) as 'PMS_PM_10', AVG(a.pms_env_1) as 'PMS_ENV_1', AVG(a.pms_env_2_5) as 'PMS_ENV_2_5', AVG(a.pms_env_10_0) as 'PMS_ENV_10', AVG(a.pms_env_0_3_c) as 'PMS_ENV_0_3_C', AVG(a.pms_env_0_5_c) as 'PMS_ENV_0_5_C', AVG(a.pms_env_1_0_c) as 'PMS_ENV_1_0_C', AVG(a.pms_env_2_5_c)  as 'PMS_ENV_2_5_C', AVG(a.pms_env_5_0_c) as 'PMS_ENV_5_0_C', AVG(a.pms_env_10_0_c)  as 'PMS_ENV_10_0_C', a.systick as 'SYSTICK', AVG(a.rssi) as 'RSSI' from measures a inner join sensors b on b.id_sensor = a.id where a.id=2 and a.timestamp between 1663941491 and 1664027891 group by a.id, DATE_FORMAT(FROM_UNIXTIME(ROUND(a.timestamp/900)*900),'%D %b %H:%i') order by FROM_UNIXTIME(a.timestamp) asc;

## dataset for sensor 11 ordered by date_time for 13.12. rounded to 15 minutes intervals (with aliases)
SELECT a.id as 'SENSOR_ID', b.place as 'PLACE', b.gps as 'GPS', AVG(a.bmp_t) as 'TEMPERATURE', AVG(a.sht_t) as 'SHT_T', AVG(a.mc_pm_1_0) as 'MC_PM_1', AVG(a.mc_pm_2_5) as 'MC_PM_2_5', AVG(a.mc_pm_4_0) as 'MC_PM_4', AVG(a.mc_pm_10) as 'MC_PM_10', AVG(a.nc_pm_0_5) as 'NC_PM_0_5', AVG(a.nc_pm_1_0) as 'NC_PM_1', AVG(a.nc_pm_2_5) as 'NC_PM_2_5', AVG(a.nc_pm_4_0) as 'NC_PM_4', AVG(a.nc_pm_10) 'NC_PM_10', AVG(a.type_particle_size) as 'PART_SIZE', AVG(a.si_lux) as 'LUX', AVG(a.si_uv) as 'UV', AVG(a.sht_hygro) as 'HYGRO', AVG(a.bmp_press) as 'PRESSURE', DATE_FORMAT(FROM_UNIXTIME(ROUND(a.timestamp/900)*900),'%D %b %H:%i') as 'DATE_TIME', AVG(a.v_bat) as 'BAT', AVG(a.energy) as 'ENERGY', AVG(a.v_in) as 'IN', AVG(a.msg_c) as 'MSG', AVG(a.pms_pm_1_0) as 'PMS_PM_1', AVG(a.pms_pm_2_5) as 'PMS_PM_2_5', AVG(a.pms_10) as 'PMS_PM_10', AVG(a.pms_env_1) as 'PMS_ENV_1', AVG(a.pms_env_2_5) as 'PMS_ENV_2_5', AVG(a.pms_env_10_0) as 'PMS_ENV_10', AVG(a.pms_env_0_3_c) as 'PMS_ENV_0_3_C', AVG(a.pms_env_0_5_c) as 'PMS_ENV_0_5_C', AVG(a.pms_env_1_0_c) as 'PMS_ENV_1_0_C', AVG(a.pms_env_2_5_c) as 'PMS_ENV_2_5_C', AVG(a.pms_env_5_0_c) as 'PMS_ENV_5_0_C', AVG(a.pms_env_10_0_c) as 'PMS_ENV_10_0_C', a.systick as 'SYSTICK', AVG(a.rssi) as 'RSSI' from measures a inner join sensors b on b.id_sensor = a.id where a.id=11 and a.timestamp between 1670886040 and 1670968072 group by a.id, DATE_FORMAT(FROM_UNIXTIME(ROUND(a.timestamp/900)*900),'%D %b %H:%i') order by FROM_UNIXTIME(a.timestamp) asc;

## KNOWAGE dataset (created by query) - about 190 rows (with aliases) - data from sensors counting vehicles, ordered by start_time for 24 hours in 15 minutes intervals
SELECT a.id_sensor as 'SENSOR_ID', b.place as 'PLACE', b.gps as 'GPS', DATE_FORMAT(a.start_time, '%D %b %H:%i') as 'START_TIME', DATE_FORMAT(a.end_time, '%D %b %H:%i') as 'END_TIME', a.counting_type as 'COUNTING_TYPE', a.result as 'RESULT' from vehicles a inner join sensors b on b.id_sensor = a.id_sensor order by a.start_time asc;

## KNOWAGE dataset (created by query) - data from sensors counting vehicles, ordered by start_time for day 13.12. in 15 minutes intervals
SELECT a.id_sensor as 'SENSOR_ID', b.place as 'PLACE', b.gps as 'GPS', DATE_FORMAT(a.start_time, '%D %b %H:%i') as 'START_TIME', DATE_FORMAT(a.end_time, '%D %b %H:%i') as 'END_TIME', a.counting_type as 'COUNTING_TYPE', a.result as 'RESULT' from vehicles a inner join sensors b on b.id_sensor = a.id_sensor where a.start_time between '2022-12-13 00:00:00' and '2022-12-13 23:00:00' order by a.start_time asc;
