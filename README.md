classDiagram
    class Utilisateur {
        -id: int
        -nom: string
        -prenom: string
        -email: string
        -motDePasse: string
        -role: string
        +seConnecter()
        +seDeconnecter()
    }

    class Administrateur {
        -permissions: string[]
        +gererStagiaires()
        +gererTuteurs()
        +consulterStatistiques()
        +gererEvaluations()
    }

    class Tuteur {
        -service: string
        -departement: string
        +evaluerStagiaire()
        +consulterStagiairesAttribues()
        +ajouterCommentaire()
    }

    class Stagiaire {
        -id: int
        -nom: string
        -prenom: string
        -adresse: string
        -telephone: string
        -age: int
        -sexe: string
        -niveauEtudes: string
        -diplome: string
        -statut: string
        +consulterProfil()
        +mettreAJourProfil()
    }

    class Stage {
        -id: int
        -dateDebut: Date
        -dateFin: Date
        -duree: int
        -typeStage: string
        -domainCompetence: string
        -service: string
        -departement: string
        -statut: string
        -estEnRetard: boolean
        +demarrerStage()
        +terminerStage()
        +prolongerStage()
    }

    class Evaluation {
        -id: int
        -note: float
        -commentaires: string
        -ameliorationsSuggrees: string
        -dateEvaluation: Date
        +ajouterEvaluation()
        +modifierEvaluation()
        +consulterEvaluation()
    }

    class Document {
        -id: int
        -nom: string
        -type: string
        -cheminFichier: string
        -dateUpload: Date
        +televerser()
        +telecharger()
        +previsualiser()
    }

    class Statistiques {
        +calculerNombreTotalStagiaires() int
        +calculerStagiairesActifs() int
        +repartitionParService() Map
        +repartitionParTypeStage() Map
        +repartitionParAge() Map
        +repartitionParSexe() Map
        +calculerNoteMoyenne() float
        +calculerDureeMoyenne() float
    }

    Utilisateur <|-- Administrateur
    Utilisateur <|-- Tuteur
    
    Stagiaire ||--o{ Stage : effectue
    Stage ||--o{ Evaluation : "est évalué par"
    Tuteur ||--o{ Evaluation : effectue
    Tuteur ||--o{ Stagiaire : supervise
    Stage ||--o{ Document : contient
    
    Administrateur ..> Statistiques : consulte
    Administrateur ..> Stagiaire : gère
    Administrateur ..> Tuteur : gère
