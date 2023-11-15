# Conception-et-modalisation-base-de-donn-es

### TP réaliser avec Patrice Elie Dit Cosaque

### Dictionnaire des données

![](Dictionnaire_des_donnees_TP.jpg)
### MCD

![](MCD_TP.jpg)

### MLD

```
Cartes = (Id_Cartes COUNTER, nom_de_la_carte VARCHAR(20));
Parties = (Id_Parties COUNTER, nom_de_la_partie VARCHAR(20), niveau_de_la_partie INT, date_de_la_partie DATE, score_de_la_partie INT, #Id_Cartes);
Equipes = (Id_Equipes COUNTER, nom_de_l_équipe VARCHAR(15));
Skins = (Id_Skins COUNTER, nom_du_skin VARCHAR(20));
Items = (Id_Items COUNTER, nom_de_l_item VARCHAR(20));
Joueurs = (Id_Joueurs COUNTER, nom_du_joueur VARCHAR(20), adresse_mail_du_joueur VARCHAR(50), date_inscription_joueur DATE, score_global_du_joueur INT, #Id_Equipes*, #Id_Parties*, #Id_Skins);
peut_détenir = (#Id_Joueurs, #Id_Items);

```

### MPD

![](MPD_TP.jpg)

### SQL

CREATE TABLE Cartes(
   Id_Cartes COUNTER,
   nom_de_la_carte VARCHAR(20),
   PRIMARY KEY(Id_Cartes)
);

CREATE TABLE Parties(
   Id_Parties COUNTER,
   nom_de_la_partie VARCHAR(20),
   niveau_de_la_partie INT,
   date_de_la_partie DATE,
   score_de_la_partie INT,
   Id_Cartes INT NOT NULL,
   PRIMARY KEY(Id_Parties),
   FOREIGN KEY(Id_Cartes) REFERENCES Cartes(Id_Cartes)
);

CREATE TABLE Equipes(
   Id_Equipes COUNTER,
   nom_de_l_équipe VARCHAR(15),
   PRIMARY KEY(Id_Equipes)
);

CREATE TABLE Skins(
   Id_Skins COUNTER,
   nom_du_skin VARCHAR(20),
   PRIMARY KEY(Id_Skins)
);

CREATE TABLE Items(
   Id_Items COUNTER,
   nom_de_l_item VARCHAR(20),
   PRIMARY KEY(Id_Items)
);

CREATE TABLE Joueurs(
   Id_Joueurs COUNTER,
   nom_du_joueur VARCHAR(20),
   adresse_mail_du_joueur VARCHAR(50),
   date_inscription_joueur DATE,
   score_global_du_joueur INT,
   Id_Equipes INT,
   Id_Parties INT,
   Id_Skins INT NOT NULL,
   PRIMARY KEY(Id_Joueurs),
   FOREIGN KEY(Id_Equipes) REFERENCES Equipes(Id_Equipes),
   FOREIGN KEY(Id_Parties) REFERENCES Parties(Id_Parties),
   FOREIGN KEY(Id_Skins) REFERENCES Skins(Id_Skins)
);

CREATE TABLE peut_détenir(
   Id_Joueurs INT,
   Id_Items INT,
   PRIMARY KEY(Id_Joueurs, Id_Items),
   FOREIGN KEY(Id_Joueurs) REFERENCES Joueurs(Id_Joueurs),
   FOREIGN KEY(Id_Items) REFERENCES Items(Id_Items)
);
