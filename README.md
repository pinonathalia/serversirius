# serversirius
import pandas as pd
import psycopg2
from sqlalchemy import create_engine


dbhost = "localhost"
dbport = "5432"
dbname = "teljohj"
dbuser = "Leo"
dbpassword = "123456"


df = pd.read_csv("4.csv", encoding="utf-8")


conn = psycopg2.connect(
    host=dbhost, port=dbport, dbname=dbname, user=dbuser, password=dbpassword
)

engine = create_engine(
    f"postgresql+psycopg2://{dbuser}:{dbpassword}@{dbhost}:{dbport}/{dbname}"
)


table_name = "nomedatabela"


df.to_sql(table_name, engine, if_exists="replace", index=False)


conn.close()
