# **Text Data Extraction from WHO Website**
## **Overview**
This script allows you to extract text data from specific pages on the World Health Organization (WHO) website, clean and tokenize the text, and create a matrix representing the occurrence of words across different pages.


| Step                           | Code                                    | Describe                                         |
|--------------------------------|-----------------------------------------|--------------------------------------------------|
| Make URLs of pages              | `# Add code`                  | Add code to collect URLs of pages                |
| Clean text of pages             | `# Add your code here`                  | Implement text cleaning for collected pages     |
| Make all text                   | `# Add your code here`                  | Combine cleaned text into a single corpus        |
| TF-IDF on all text              | `# Add your code here`                  | Apply TF-IDF transformation to the text corpus  |
| Make page-word matrix           | `# Add your code here`                  | Create a matrix representing pages and words    |
| Visualizations                 | `# Add your code here`                  | Generate visualizations for analysis            |
| Implement model co-clustering   | `# Add your code here`                  | Apply co-clustering algorithm to the data       |


## **Steps**
1. **URLs of pages**: Edit the list of URLs in the script to specify the WHO website pages you want to analyze.
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

| No. | Topic                                                | URL                                                                                                                                       |
|-----|------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | Abortion                                             | [https://www.who.int/health-topics/abortion#tab=tab_1](https://www.who.int/health-topics/abortion#tab=tab_1)                                |
| 2   | Addictive Behaviour                                   | [https://www.who.int/health-topics/addictive-behaviour#tab=tab_1](https://www.who.int/health-topics/addictive-behaviour#tab=tab_1)        |
| 3   | Adolescent Health                                     | [https://www.who.int/health-topics/adolescent-health#tab=tab_1](https://www.who.int/health-topics/adolescent-health#tab=tab_1)              |
| 4   | Ageing                                               | [https://www.who.int/health-topics/ageing#tab=tab_1](https://www.who.int/health-topics/ageing#tab=tab_1)                                  |
| 5   | Ageism                                               | [https://www.who.int/health-topics/ageism#tab=tab_1](https://www.who.int/health-topics/ageism#tab=tab_1)                                  |
| 6   | Air Pollution                                        | [https://www.who.int/health-topics/air-pollution#tab=tab_1](https://www.who.int/health-topics/air-pollution#tab=tab_1)                    |
| 7   | Alcohol                                              | [https://www.who.int/health-topics/alcohol#tab=tab_1](https://www.who.int/health-topics/alcohol#tab=tab_1)                                |
| 8   | Anaemia                                              | [https://www.who.int/health-topics/anaemia#tab=tab_1](https://www.who.int/health-topics/anaemia#tab=tab_1)                                |
| 9   | Antimicrobial Resistance                              | [https://www.who.int/health-topics/antimicrobial-resistance#tab=tab_1](https://www.who.int/health-topics/antimicrobial-resistance#tab=tab_1)|
| 10  | Assistive Technology                                  | [https://www.who.int/health-topics/assistive-technology#tab=tab_1](https://www.who.int/health-topics/assistive-technology#tab=tab_1)        |
| 11  | Biological Weapons                                    | [https://www.who.int/health-topics/biological-weapons#tab=tab_1](https://www.who.int/health-topics/biological-weapons#tab=tab_1)          |
| 12  | Biologicals                                           | [https://www.who.int/health-topics/biologicals#tab=tab_1](https://www.who.int/health-topics/biologicals#tab=tab_1)                        |
| 13  | Blood Products                                        | [https://www.who.int/health-topics/blood-products#tab=tab_1](https://www.who.int/health-topics/blood-products#tab=tab_1)                  |
| 14  | Blood Transfusion Safety                               | [https://www.who.int/health-topics/blood-transfusion-safety#tab=tab_1](https://www.who.int/health-topics/blood-transfusion-safety#tab=tab_1)|
| 15  | Brain Health                                          | [https://www.who.int/health-topics/brain-health#tab=tab_1](https://www.who.int/health-topics/brain-health#tab=tab_1)                      |
| 16  | Breastfeeding                                         | [https://www.who.int/health-topics/breastfeeding#tab=tab_1](https://www.who.int/health-topics/breastfeeding#tab=tab_1)                    |
| 17  | Buruli Ulcer                                          | [https://www.who.int/health-topics/buruli-ulcer#tab=tab_1](https://www.who.int/health-topics/buruli-ulcer#tab=tab_1)                      |
| 18  | Cancer                                               | [https://www.who.int/health-topics/cancer#tab=tab_1](https://www.who.int/health-topics/cancer#tab=tab_1)                                  |
| 19  | Cardiovascular Diseases                               | [https://www.who.int/health-topics/cardiovascular-diseases#tab=tab_1](https://www.who.int/health-topics/cardiovascular-diseases#tab=tab_1)|
| 20  | Cervical Cancer                                       | [https://www.who.int/health-topics/cervical-cancer#tab=tab_1](https://www.who.int/health-topics/cervical-cancer#tab=tab_1)                |
| 21  | Chagas Disease                                        | [https://www.who.int/health-topics/chagas-disease#tab=tab_1](https://www.who.int/health-topics/chagas-disease#tab=tab_1)                  |
| 22  | Chemical Incidents                                     | [https://www.who.int/health-topics/chemical-incidents#tab=tab_1](https://www.who.int/health-topics/chemical-incidents#tab=tab_1)            |
| 23  | Chemical Safety                                       | [https://www.who.int/health-topics/chemical-safety#tab=tab_1](https://www.who.int/health-topics/chemical-safety#tab=tab_1)                |
| 24  | Chikungunya                                           | [https://www.who.int/health-topics/chikungunya#tab=tab_1](https://www.who.int/health-topics/chikungunya#tab=tab_1)                        |
| 25  | Child Growth                                          | [https://www.who.int/health-topics/child-growth#tab=tab_1](https://www.who.int/health-topics/child-growth#tab=tab_1)                      |
| 26  | Child Health                                          | [https://www.who.int/health-topics/child-health#tab=tab_1](https://www.who.int/health-topics/child-health#tab=tab_1)                      |
| 27  | Children Environmental Health                          | [https://www.who.int/health-topics/children-environmental-health#tab=tab_1](https://www.who.int/health-topics/children-environmental-health#tab=tab_1)|
| 28  | Cholera                                               | [https://www.who.int/health-topics/cholera#tab=tab_1](https://www.who.int/health-topics/cholera#tab=tab_1)                                |
| 29  | Chronic Respiratory Diseases                           | [https://www.who.int/health-topics/chronic-respiratory-diseases#tab=tab_1](https://www.who.int/health-topics/chronic-respiratory-diseases#tab=tab_1)|
| 30  | Climate Change                                         | [https://www.who.int/health-topics/climate-change#tab=tab_1](https://www.who.int/health-topics/climate-change#tab=tab_1)                   |
| 31  | Clinical Trials                                        | [https://www.who.int/health-topics/clinical-trials#tab=tab_1](https://www.who.int/health-topics/clinical-trials#tab=tab_1)                 |
| 32  | Commercial Determinants of Health                      | [https://www.who.int/health-topics/commercial-determinants-of-health#tab=tab_1](https://www.who.int/health-topics/commercial-determinants-of-health#tab=tab_1)|
| 33  | Common Goods for Health                                 | [https://www.who.int/health-topics/common-goods-for-health#tab=tab_1](https://www.who.int/health-topics/common-goods-for-health#tab=tab_1)|
| 34  | Complementary Feeding                                   | [https://www.who.int/health-topics/complementary-feeding#tab=tab_1](https://www.who.int/health-topics/complementary-feeding#tab=tab_1)    |
| 35  | Congenital Disorders                                    | [https://www.who.int/health-topics/congenital-disorders#tab=tab_1](https://www.who.int/health-topics/congenital-disorders#tab=tab_1)      |
| 36  | Contraception                                           | [https://www.who.int/health-topics/contraception#tab=tab_1](https://www.who.int/health-topics/contraception#tab=tab_1)                    |
| 37  | Coronavirus                                            | [https://www.who.int/health-topics/coronavirus#tab=tab_1](https://www.who.int/health-topics/coronavirus#tab=tab_1)                        |
| 38  | Crimean-Congo Haemorrhagic Fever                       | [https://www.who.int/health-topics/crimean-congo-haemorrhagic-fever#tab=tab_1](https://www.who.int/health-topics/crimean-congo-haemorrhagic-fever#tab=tab_1)|
| 39  | Deafness and Hearing Loss                               | [https://www.who.int/health-topics/deafness-and-hearing-loss#tab=tab_1](https://www.who.int/health-topics/deafness-and-hearing-loss#tab=tab_1)|
| 40  | Deliberate Events                                       | [https://www.who.int/health-topics/deliberate-events#tab=tab_1](https://www.who.int/health-topics/deliberate-events#tab=tab_1)            |
| 41  | Dementia                                               | [https://www.who.int/health-topics/dementia#tab=tab_1](https://www.who.int/health-topics/dementia#tab=tab_1)                                |
| 42  | Dengue and Severe Dengue                               | [https://www.who.int/health-topics/dengue-and-severe-dengue#tab=tab_1](https://www.who.int/health-topics/dengue-and-severe-dengue#tab=tab_1)|
| 43  | Depression                                             | [https://www.who.int/health-topics/depression#tab=tab_1](https://www.who.int/health-topics/depression#tab=tab_1)                          |
| 44  | Diabetes                                               | [https://www.who.int/health-topics/diabetes#tab=tab_1](https://www.who.int/health-topics/diabetes#tab=tab_1)                              |
| 45  | Diarrhoea                                              | [https://www.who.int/health-topics/diarrhoea#tab=tab_1](https://www.who.int/health-topics/diarrhoea#tab=tab_1)                            |
| 46  | Digital Health                                          | [https://www.who.int/health-topics/digital-health#tab=tab_1](https://www.who.int/health-topics/digital-health#tab=tab_1)                  |
| 47  | Diphtheria                                              | [https://www.who.int/health-topics/diphtheria#tab=tab_1](https://www.who.int/health-topics/diphtheria#tab=tab_1)                          |
| 48  | Disability                                               | [https://www.who.int/health-topics/disability#tab=tab_1](https://www.who.int/health-topics/disability#tab=tab_1)                          |
| 49  | Dracunculiasis                                          | [https://www.who.int/health-topics/dracunculiasis#tab=tab_1](https://www.who.int/health-topics/dracunculiasis#tab=tab_1)                  |
| 50  | Drought                                                   | [https://www.who.int/health-topics/drought#tab=tab_1](https://www.who.int/health-topics/drought#tab=tab_1)                                |
| 51  | Drowning                                                 | [https://www.who.int/health-topics/drowning#tab=tab_1](https://www.who.int/health-topics/drowning#tab=tab_1)                              |
| 52  | Drugs                                                    | [https://www.who.int/health-topics/drugs2#tab=tab_1](https://www.who.int/health-topics/drugs2#tab=tab_1)                                |
| 53  | Earthquakes                                              | [https://www.who.int/health-topics/earthquakes#tab=tab_1](https://www.who.int/health-topics/earthquakes#tab=tab_1)                        |

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





```python
import re
import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer

Pages = """
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


import re

# Extract terms using regular expression
terms = re.findall(r'\b[A-Za-z\s-]+\b', Pages)

# Remove duplicates
unique_terms = list(set(terms))

# Print the list of terms
for term in unique_terms:
    print(term)


#page_names = ["Page 1", "Page 2", "Page 3", "Page 4", "Page 5", "Page 6", "Page 7"]


def clean_text(text):
    # Remove newline characters
    cleaned_text = text.replace('\n', '')

    # Remove numbers
    cleaned_text = re.sub(r'\d+', '', cleaned_text)

    # Add spaces between words (split on uppercase letters)
    cleaned_text = re.sub(r'([a-z])([A-Z])', r'\1 \2', cleaned_text)

    # Remove non-alphabetic characters (punctuation, symbols, etc.)
    cleaned_text = re.sub(r'[^a-zA-Z\s]', '', cleaned_text)

    # Remove specific word
    cleaned_text = cleaned_text.replace('ABCDEFGHIJKLMNOPQRSTUVWXYZRegions', 'regions')
    cleaned_text = cleaned_text.replace('abcdefghijklmnopqrstuvwxyzregions', 'regions')
    cleaned_text = cleaned_text.replace('ABCDEFGHIJKLMNOPQRSTUVWXYZResources', 'resources')
    cleaned_text = cleaned_text.replace('EnglishFranaisEspaol', 'English Franais Espaol')

    cleaned_text = cleaned_text.replace('Epidemiological', '')
    cleaned_text = cleaned_text.replace('healthsupportive', 'health supportive')
    cleaned_text = cleaned_text.replace('selectSelect', 'select')
    cleaned_text = cleaned_text.replace('healthsupportive', '')
    cleaned_text = cleaned_text.replace('solutionssupporting', 'solutions supporting')
    cleaned_text = cleaned_text.replace('environmentensuring', 'environment ensuring')
    cleaned_text = cleaned_text.replace('environmentrelated', 'environment related')
    cleaned_text = cleaned_text.replace('includeproviding', 'include providing')
    cleaned_text = cleaned_text.replace('whoabout', 'who about')
    cleaned_text = cleaned_text.replace('whoclassifications', 'who classifications')
    cleaned_text = cleaned_text.replace('whoilo', '')
    cleaned_text = cleaned_text.replace('whopartnerships', 'who partner ships')

    

    return cleaned_text
# Example usage:

# Clean each text in the list
cleaned_texts = [clean_text(text) for text in all_texts]



# Initialize the CountVectorizer
vectorizer = CountVectorizer()

# Fit and transform the cleaned texts into a document-word matrix
document_word_matrix = vectorizer.fit_transform(cleaned_texts)

# Get feature names (words) from the vectorizer
feature_names = vectorizer.get_feature_names()

# Convert the document-word matrix to a DataFrame
df_document_word_matrix = pd.DataFrame(document_word_matrix.toarray(), columns=feature_names)

# Add a column for page names
df_document_word_matrix.insert(0, "Page Name", page_names)

# Print the DataFrame
print(df_document_word_matrix)
df_document_word_matrix

# Print the cleaned texts
for cleaned_text in cleaned_texts:
    print(cleaned_text)
    
```




```python
from wordcloud import WordCloud
import matplotlib.pyplot as plt
import numpy as np

# Example feature_names (replace with your actual data)
#feature_names = ['word1', 'word2', 'word3', 'word4', 'word5']

# Convert feature_names to a string for word cloud generation
text = ' '.join(feature_names)

# Generate a word cloud
wordcloud = WordCloud(width=800, height=800,
                      background_color='black',
                      colormap='Reds',  # You can choose other colormaps
                      contour_color='red',
                      contour_width=1,
                      mode='RGBA'
                      #rotation_range=0  # Set rotation_range to zero for horizontal layout
                      #mask=np.array(plt.imread("circle_mask.png")),  # Replace with your circular mask image
                      ).generate(text)

# Display the generated word cloud using matplotlib
plt.figure(figsize=(8, 8), facecolor=None)
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis("off")
plt.tight_layout(pad=0)

# Show the word cloud
plt.show()

```
