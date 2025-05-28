# Système de Gestion des Stages

## Diagramme de Classes

```mermaid
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
    
    %% Relations d'héritage
    Utilisateur <|-- Administrateur
    Utilisateur <|-- Tuteur
    
    %% Relations d'association
    Stagiaire ||--o{ Stage
    Stage ||--o{ Evaluation
    Tuteur ||--o{ Evaluation
    Tuteur ||--o{ Stagiaire
    Stage ||--o{ Document
    
    %% Relations de dépendance
    Administrateur ..> Statistiques
    Administrateur ..> Stagiaire
    Administrateur ..> Tuteur
