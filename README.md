# rims_db_definition

## Notes

- Decisió relació persona/grup recerca. Per exemple, a PROJECT cal tenir el research_group_id, quan ja està disponible a través de main_researcher_id? El mateix passa a ACTIVITY

- PERSON és sempre gent, o poden ser organitzacions?

## Esquema

```mermaid
erDiagram
PERSON{
    int id
    int research_group_id
    int person_type
}

RESEARCH_GROUP{
    int id
}

PROJECT{
    int id
    string title
    int main_researcher_id
    int research_group_id
    string founding_programme
    date start_date
    date end_date

}

STAKEHOLDERS_PROJECT{
    int project_id
    int person_id
}

PEOPLE_INVOLVED_PROJECT{
    int project_id
    int person_id
}

ACTIVITY{
    int id
    int related_project_id
    int related_person_id
    string title
    date date
    string description
    int stakeholders_type
    int interaction_type
    int activity_type
    string evidence
}

CREAF_STAFF_ACTIVITY{
    int activity_id
    int person_id
}

OUTPUT{
    int id
    int related_project_id
    int related_person_id
    int related_activity_id
    int output_type
    string title
    date date
    int stakeholder_interaction
    string description
    string link
}

STAKEHOLDERS_OUTCOME{
    int outcome_id
    int person_id
}

OUTCOME{
    int id
    int related_output_id
    int related_activity_id
    date date
    int outcome_type
    string description
    string evidence
}

IMPACT{
    int id
    int related_outcome_id
    date date
    int impact_type
    string description
    int role_played_by_research_team
    string evidence
    int confidence_level
    int contribution_type
}

STAKEHOLDERS_IMPACT{
    int impact_id
    int person_id
}

CREAF_STAFF_IMPACT{
    int impact_id
    int person_id
}

RESEARCH_GROUP ||--o{ PERSON : "Belongs to"
PROJECT ||--o{ PERSON : "Main researcher for"
PROJECT ||--o{ RESEARCH_GROUP: "Group doing research for the project"
STAKEHOLDERS_PROJECT ||--o{ PERSON : "Stakeholder in"
STAKEHOLDERS_PROJECT ||--o{ PROJECT : "Project in which stakes are held"
PEOPLE_INVOLVED_PROJECT ||--o{ PERSON : "Involved in"
PEOPLE_INVOLVED_PROJECT ||--o{ PROJECT : "Project in which person is involved"
ACTIVITY ||--o{ PERSON : "Person related to activity" 
ACTIVITY ||--o{ PROJECT : "Project related to activity" 
CREAF_STAFF_ACTIVITY ||--o{ PERSON : "CREAF staff involved in activity"
CREAF_STAFF_ACTIVITY ||--o{ ACTIVITY : "Activity in which someone from CREAF is involved"
OUTPUT ||--o{ PROJECT: "Project related to output"
OUTPUT ||--o{ PERSON: "Person related to output"
OUTCOME ||--o{ OUTPUT: "Related output"
OUTCOME ||--o{ ACTIVITY: "Related activity"
STAKEHOLDERS_OUTCOME ||--o{ OUTCOME: "Outcome stakeholders"
STAKEHOLDERS_OUTCOME ||--o{ PERSON: "Stakeholder in outcome"
STAKEHOLDERS_IMPACT ||--o{ OUTCOME: "Outcome impact"
STAKEHOLDERS_IMPACT ||--o{ PERSON: "Stakeholder in impact"
CREAF_STAFF_IMPACT ||--o{ PERSON : "CREAF staff involved in impact"
CREAF_STAFF_IMPACT ||--o{ IMPACT : "Impact in which someone from CREAF is involved"
```