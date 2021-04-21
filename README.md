import pandas as pd

client = pd.read_csv('')


test = client.head()


def insert_to_client (client) :
    
    import sqlite3

    #je me connect avec la base
    conn = sqlite3.connect('database_fraud.db')
    
    #instaciation d'un curseur
    curs = conn.cursor()


    for i in range(len(client) -1) :

        enreg = (client.disrict.loc[i],client.client_id.loc[i],client.client_catg.loc[i],client.region.loc[i],client.creation_date.loc[i],client.target.loc[i])

        #la requette d'insertion dans notre base
        req = f"INSERT INTO clients values {enreg}"

        #execution de la requette par le curseur
        curs.execute(req)

        #je commmit maintenant pour envoyé la requete dans la db
        conn.commit()
    
    #je ferme la connection
    conn.close()

    return "good"
