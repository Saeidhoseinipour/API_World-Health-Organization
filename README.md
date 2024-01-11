# **Text Data Extraction from WHO Website**
## **Overview**
This script allows you to extract text data from specific pages on the World Health Organization (WHO) website, clean and tokenize the text, and create a matrix representing the occurrence of words across different pages.

Steps
1. Define URLs: Edit the list of URLs in the script to specify the WHO website pages you want to analyze.
```python
import import numpy as np

Page_names = """
Health interventions_Abortion
Human behaviour_Addictive behaviour
Populations and demographics_Adolescent health
Populations and demographics_Ageing
Other_Ageism
Physical environment_Air pollution
Other_Alcohol
Conditions_Anaemia
Physical environment_Antimicrobial resistance
Health interventions_Assistive technology
Other_Biological weapons
Substances_Biologicals
Physiological interventions_Blood products
Health systems_Blood transfusion safety
Health and wellbeing_Brain health
Health interventions_Breastfeeding
Communicable diseases_Buruli ulcer (Mycobacterium ulcerans infection)
Non-communicable diseases_Cancer
Diseases and conditions_Cardiovascular diseases
Non-communicable diseases_Cervical cancer
Diseases and conditions_Chagas disease (American trypanosomiasis)
Disasters_Chemical incidents
Physical environment_Chemical safety
Diseases and conditions_Chikungunya
Health and wellbeing_Child growth
Populations and demographics_Child health
Physical environment_Children's environmental health
Diseases and conditions_Cholera
Non-communicable diseases_Chronic respiratory diseases
Disasters_Climate change
Health systems_Clinical trials
Socio-political determinants_Commercial determinants of health
Health systems_Common goods for health
Health interventions_Complementary feeding
Diseases and conditions_Congenital disorders
Health interventions_Contraception
Communicable diseases_Coronavirus disease (COVID-19)
Communicable diseases_Crimean-Congo haemorrhagic fever
Conditions_Deafness and hearing loss
Physical environment_Deliberate events
Diseases and conditions_Dementia
Diseases and conditions_Dengue and severe dengue
Conditions_Depression
Diseases and conditions_Diabetes
Diseases and conditions_Diarrhoea
Health systems_Digital health
Communicable diseases_Diphtheria
Populations and demographics_Disability
Diseases and conditions_Dracunculiasis (Guinea-worm disease)
Disasters_Drought
Injuries_Drowning
Substances_Drugs (psychoactive)
Disasters_Earthquakes
Communicable diseases_Ebola virus disease
Diseases and conditions_Echinococcosis
Physical environment_Electromagnetic fields
Health systems_Emergency care
Other_Energy and health
Physical environment_Environmental health
Diseases and conditions_Epilepsy
Diseases and conditions_Eye care, vision impairment and blindness
Human behaviour_Female genital mutilation
Health systems_Financial protection
Disasters_Floods
Other_Food fortification
Physical environment_Food safety
Diseases and conditions_Foodborne diseases
Diseases and conditions_Foodborne trematode infections
Socio-political determinants_Gender and health
Health systems_Genomics
Socio-political determinants_Global health ethics
Health systems_Health accounts
Health systems_Health budget
Other_Health economics
Other_Health equity
Health systems_Health financing
Health interventions_Health impact assessment
Behavioural interventions_Health promoting schools
Behavioural interventions_Health promotion
Socio-political determinants_Health security
Health systems_Health system governance
Health systems_Health taxes
Other_Health technology assessment
Health systems_Health workforce
Human behaviour_Healthy diet
Disasters_Heatwaves
Communicable diseases_Hepatitis
Communicable diseases_HIV
Health systems_Hospitals
Diseases and conditions_Human African trypanosomiasis (sleeping sickness)
Other_Human genome editing
Socio-political determinants_Human rights
Diseases and conditions_Hypertension
Health interventions_In vitro diagnostics
Health interventions_Infant nutrition
Health systems_Infection prevention and control
Conditions_Infertility
Diseases and conditions_Influenza (avian and other zoonotic)
Diseases and conditions_Influenza seasonal
Socio-political determinants_Infodemic
Socio-political determinants_Intellectual property and trade
Socio-political determinants_International Health Regulations
Disasters_Landslides
Communicable diseases_Lassa fever
Other_Lead poisoning
Diseases and conditions_Leishmaniasis
Diseases and conditions_Leprosy (Hansen's disease)
Diseases and conditions_Lymphatic filariasis (Elephantiasis)
Diseases and conditions_Malaria
Diseases and conditions_Malnutrition
Communicable diseases_Marburg virus disease
Populations and demographics_Maternal health
Diseases and conditions_Measles
Health interventions_Medical devices
Health interventions_Medicines
Communicable diseases_Meningitis
Health and wellbeing_Mental health
Substances_Micronutrients
Communicable diseases_Middle East respiratory syndrome coronavirus (MERS-CoV)
Diseases and conditions_Mpox (monkeypox)
Diseases and conditions_Mycetoma, chromoblastomycosis and other deep mycoses
Other_Neglected tropical diseases
Populations and demographics_Newborn health
Communicable diseases_Nipah virus infection
Diseases and conditions_Noncommunicable diseases
Health systems_Nursing and Midwifery
Human behaviour_Nutrition
Conditions_Obesity
Physical environment_Occupational health
Diseases and conditions_Onchocerciasis (river blindness)
Health interventions_One health
Health and wellbeing_Oral health
Other_Oxygen
Health systems_Palliative care
Health systems_Patient safety
Diseases and conditions_Pertussis
Human behaviour_Physical activity
Diseases and conditions_Plague
Diseases and conditions_Pneumonia
Diseases and conditions_Poliomyelitis (polio)
Health systems_Primary health care
Health systems_Quality of care
Diseases and conditions_Rabies
Physical environment_Radiation
Disasters_Radiation emergencies
Substances_Radon
Populations and demographics_Refugee and migrant health
Health interventions_Rehabilitation
Health systems_Research
Communicable diseases_Rift valley fever
Physical environment_Road traffic injuries
Diseases and conditions_Scabies
Diseases and conditions_Schistosomiasis (Bilharzia)
Human behaviour_Self-care interventions for health
Diseases and conditions_Sepsis
Communicable diseases_Severe Acute Respiratory Syndrome (SARS)
Health and wellbeing_Sexual health
Diseases and conditions_Sexually transmitted infections (STIs)
Communicable diseases_Smallpox
Diseases and conditions_Snakebite envenoming
Socio-political determinants_Social determinants of health
Diseases and conditions_Soil-transmitted helminthiases
Conditions_Stillbirth
Health systems_Substandard and falsified medical products
Health interventions_Suicide prevention
Socio-political determinants_Sustainable development
Diseases and conditions_Syphilis
Diseases and conditions_Taeniasis and cysticercosis
Diseases and conditions_Tetanus
Diseases and conditions_Tick-borne encephalitis
Substances_Tobacco
Diseases and conditions_Trachoma
Health interventions_Traditional, Complementary and Integrative Medicine
Health interventions_Transplantation
Socio-political determinants_Travel and health
Disasters_Tropical Cyclones
Disasters_Tsunamis
Diseases and conditions_Tuberculosis
Diseases and conditions_Typhoid
Physical environment_Ultraviolet radiation
Other_Universal health coverage
Socio-political determinants_Urban health
Health interventions_Vaccines and immunization
Human behaviour_Violence against children
Human behaviour_Violence against women
Disasters_Volcanic eruptions
Physical environment_Water, sanitation and hygiene (WASH)
Disasters_Wildfires
Populations and demographics_Women's health
Diseases and conditions_Yaws (Endemic treponematoses)
Communicable diseases_Yellow fever
Other_Zika virus disease
"""
```


```python
import numpy as np

# Split the Page_names variable into lines
page_lines = Page_names.strip().split('\n')

# Create a list to store the URLs
pages = []

# Iterate over each line and extract information
for line in page_lines:
    # Split each line into parts using the underscore character
    parts = line.split('_')
    
    # Extract the topic and create the URL
    topic = parts[-1].strip()
    if topic:
        # Replace spaces with hyphens in the topic
        topic_with_hyphens = topic.replace(' ', '-')
        url = f'https://www.who.int/health-topics/{topic_with_hyphens.lower()}#tab=tab_1'
        pages.append(url)

# Print the list of URLs
#for page in pages:
#    print(page)


    
pages[16] = 'https://www.who.int/health-topics/buruli-ulcer#tab=tab_1'
pages[20] = 'https://www.who.int/health-topics/chagas-disease#tab=tab_1'
pages[26] = 'https://www.who.int/health-topics/children-environmental-health#tab=tab_1'
pages[36] = 'https://www.who.int/health-topics/coronavirus#tab=tab_1'
pages[48] = 'https://www.who.int/health-topics/dracunculiasis#tab=tab_1'
pages[51] = 'https://www.who.int/health-topics/drugs2#tab=tab_1'
#= 'https://www.who.int/health-topics/modified-url-1#tab=tab_1'
#pages[1] = 'https://www.who.int/health-topics/modified-url-2#tab=tab_1'
print(np.shape(pages),pages)
```
