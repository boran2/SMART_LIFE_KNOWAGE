# SMART_LIFE_KNOWAGE


## MARIA DB - connection and creating smart_life database
download MARIADB 10.9

login: mysql -u root -padmin

from maria db command prompt run zipped mariaDB_dump.sql

## KNOWAGE data source
url: jdbc:mariadb://localhost:3306/smart_life?user=root&password=admin

driver: org.mariadb.jdbc.Driver

user: root
password: admin

## KNOWAGE dataset (created by query) - over 7400 rows 
SELECT a.id, b.place, b.gps, AVG(a.bmp_t), AVG(a.sht_t), AVG(a.mc_pm_1_0), AVG(a.mc_pm_2_5), AVG(a.mc_pm_4_0), AVG(a.mc_pm_10), AVG(a.nc_pm_0_5), AVG(a.nc_pm_1_0), AVG(a.nc_pm_2_5), AVG(a.nc_pm_4_0), AVG(a.nc_pm_10), AVG(a.type_particle_size), AVG(a.si_lux), AVG(a.si_uv), AVG(a.sht_hygro), AVG(a.bmp_press), a.timestamp, AVG(a.v_bat), AVG(a.energy), AVG(a.v_in), AVG(a.msg_c), AVG(a.pms_pm_1_0), AVG(a.pms_pm_2_5), AVG(a.pms_10), AVG(a.pms_env_1), AVG(a.pms_env_2_5), AVG(a.pms_env_10_0), AVG(a.pms_env_0_3_c), AVG(a.pms_env_0_5_c), AVG(a.pms_env_1_0_c), AVG(a.pms_env_2_5_c), AVG(a.pms_env_5_0_c), AVG(a.pms_env_10_0_c), a.systick, AVG(a.rssi) from measures a inner join sensors b on b.id_sensor = a.id group by a.timestamp order by a.timestamp asc;

## alternative KNOWAGE dataset (created by query) - over 5300 rows with aliases to better display in knowage
SELECT a.id as 'MEASURE_ID', b.place as 'PLACE', b.gps as 'GPS', AVG(a.bmp_t) as 'TEMPERATURE', AVG(a.sht_t) as 'SHT_T', AVG(a.mc_pm_1_0) as 'MC_PM_1', AVG(a.mc_pm_2_5) as 'MC_PM_2.5', AVG(a.mc_pm_4_0)  as 'MC_PM_4', AVG(a.mc_pm_10) as 'MC_PM_10', AVG(a.nc_pm_0_5) as 'NC_PM_0.5', AVG(a.nc_pm_1_0) as 'NC_PM_1', AVG(a.nc_pm_2_5) as 'NC_PM_2.5', AVG(a.nc_pm_4_0) as 'NC_PM_4', AVG(a.nc_pm_10) as 'NC_PM_10', AVG(a.type_particle_size) as 'PART_SIZE', AVG(a.si_lux) as 'LUX', AVG(a.si_uv) as 'UV', AVG(a.sht_hygro) as 'HYGRO', AVG(a.bmp_press) as 'PRESSURE', ROUND(a.timestamp/1000,2)  as 'TIMESTAMP', AVG(a.v_bat) as 'BAT', AVG(a.energy) as 'ENERGY', AVG(a.v_in)  as 'IN', AVG(a.msg_c) as 'MSG_C', AVG(a.pms_pm_1_0) as 'PMS_PM_1', AVG(a.pms_pm_2_5) as 'PMS_PM_2.5', AVG(a.pms_10) as 'PMS_PM_10', AVG(a.pms_env_1)  as 'PMS_ENV_1', AVG(a.pms_env_2_5) as 'PMS_ENV_2.5', AVG(a.pms_env_10_0) as 'PMS_ENV_10', AVG(a.pms_env_0_3_c) as 'PMS_ENV_0.3_C', AVG(a.pms_env_0_5_c) as 'PMS_ENV_0.5_C', AVG(a.pms_env_1_0_c) as 'PMS_ENV_1_C', AVG(a.pms_env_2_5_c) as 'PMS_ENV_2.5_C', AVG(a.pms_env_5_0_c)  as 'PMS_ENV_5_C', AVG(a.pms_env_10_0_c)  as 'PMS_ENV_10_C', a.systick as 'SYSTICK', AVG(a.rssi) as 'RSSI' from measures a inner join sensors b on b.id_sensor = a.id group by ROUND(a.timestamp/1000,2) order by ROUND(a.timestamp/1000,2) asc;

## if we have small number of sensors, we can create dataset for each sensor ordered by timestamp from altrenative dataset
SELECT a.id as 'MEASURE_ID', b.place as 'PLACE', b.gps as 'GPS', AVG(a.bmp_t) as 'TEMPERATURE', AVG(a.sht_t) as 'SHT_T', AVG(a.mc_pm_1_0) as 'MC_PM_1', AVG(a.mc_pm_2_5) as 'MC_PM_2.5', AVG(a.mc_pm_4_0)  as 'MC_PM_4', AVG(a.mc_pm_10) as 'MC_PM_10', AVG(a.nc_pm_0_5) as 'NC_PM_0.5', AVG(a.nc_pm_1_0) as 'NC_PM_1', AVG(a.nc_pm_2_5) as 'NC_PM_2.5', AVG(a.nc_pm_4_0) as 'NC_PM_4', AVG(a.nc_pm_10) as 'NC_PM_10', AVG(a.type_particle_size) as 'PART_SIZE', AVG(a.si_lux) as 'LUX', AVG(a.si_uv) as 'UV', AVG(a.sht_hygro) as 'HYGRO', AVG(a.bmp_press) as 'PRESSURE', ROUND(a.timestamp/1000,2)  as 'TIMESTAMP', AVG(a.v_bat) as 'BAT', AVG(a.energy) as 'ENERGY', AVG(a.v_in)  as 'IN', AVG(a.msg_c) as 'MSG_C', AVG(a.pms_pm_1_0) as 'PMS_PM_1', AVG(a.pms_pm_2_5) as 'PMS_PM_2.5', AVG(a.pms_10) as 'PMS_PM_10', AVG(a.pms_env_1)  as 'PMS_ENV_1', AVG(a.pms_env_2_5) as 'PMS_ENV_2.5', AVG(a.pms_env_10_0) as 'PMS_ENV_10', AVG(a.pms_env_0_3_c) as 'PMS_ENV_0.3_C', AVG(a.pms_env_0_5_c) as 'PMS_ENV_0.5_C', AVG(a.pms_env_1_0_c) as 'PMS_ENV_1_C', AVG(a.pms_env_2_5_c) as 'PMS_ENV_2.5_C', AVG(a.pms_env_5_0_c)  as 'PMS_ENV_5_C', AVG(a.pms_env_10_0_c)  as 'PMS_ENV_10_C', a.systick as 'SYSTICK', AVG(a.rssi) as 'RSSI' from measures a inner join sensors b on b.id_sensor = a.id where a.id=2 group by ROUND(a.timestamp/1000,2) order by ROUND(a.timestamp/1000,2) asc;
