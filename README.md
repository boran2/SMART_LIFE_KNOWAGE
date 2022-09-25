# SMART_LIFE_KNOWAGE

## MARIA DB - connection and creating smart_life database
download MARIADB 10.9
from maria db command prompt run zipped mariaDB_dump.sql

## KNOWAGE data source
url: jdbc:mariadb://localhost:3306/smart_life?user=root&password=admin

driver: org.mariadb.jdbc.Driver

user: root
password: admin

## KNOWAGE dataset (created by query)
SELECT a.id, b.place, b.gps_lat, b.gps_long, AVG(a.bmp_t), AVG(a.sht_t), AVG(a.mc_pm_1_0), AVG(a.mc_pm_2_5), AVG(a.mc_pm_4_0), AVG(a.mc_pm_10), AVG(a.nc_pm_0_5), AVG(a.nc_pm_1_0), AVG(a.nc_pm_2_5), AVG(a.nc_pm_4_0), AVG(a.nc_pm_10), AVG(a.type_particle_size), AVG(a.si_lux), AVG(a.si_uv), AVG(a.sht_hygro), AVG(a.bmp_press), a.timestamp, AVG(a.v_bat), AVG(a.energy), AVG(a.v_in), AVG(a.msg_c), AVG(a.pms_pm_1_0), AVG(a.pms_pm_2_5), AVG(a.pms_10), AVG(a.pms_env_1), AVG(a.pms_env_2_5), AVG(a.pms_env_10_0), AVG(a.pms_env_0_3_c), AVG(a.pms_env_0_5_c), AVG(a.pms_env_1_0_c), AVG(a.pms_env_2_5_c), AVG(a.pms_env_5_0_c), AVG(a.pms_env_10_0_c), a.systick, AVG(a.rssi) from measures a inner join sensors b on b.id_sensor = a.id group by a.timestamp order by a.timestamp asc;
