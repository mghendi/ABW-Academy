## Crime Prediction and hotspot identification in Nigeria

#### Background information
Crime is global phenomena that need to be tackled to create an enabling environment for socio-economic development. Crime does not only pose threats to
the lives and properties of citizens, but affect the overall development of a nation. Thus, there is a strong link between crime and   development. 
Globalization has enhanced the connectivity of persons which has enabled criminal elements to organize and perpetrate large-scale crimes. Nigeria has arguably become one of the epicenters of crimes with insecurity rising at an alarming rate in recent years.
Peace and stability have been the core objective of most nations in the world over the years, crimes have continued to remain a major setback
to achieving meaningful socio-economic development in Nigeria. In recent time, Nigeria had continued to witness a tremendous setback in its socio-economic development fuelled by the continuous resurgence of different kinds of crimes threats particularly armed banditry, kidnapping, terrorism, maritime crime, human trafficking, drugs trafficking, fire arms trafficking, Cybercrime, grand corruption, wildlife crime among others thereby posing a serious threat to the country’s national security. All the 6 Geo-political zones and 36 States in Nigeria are facing different types of crimes and Nigerian government have spent trillion of Naira on national security over the past five years. The governments’ effort to bring the menace to a standstill to avoid total possible breakdown of law and order seems not to have yielded the desired positive result.



#### Goal of the project
- To identify types of crimes prevalent in Nigeria 
- To Predict crime-rates 
- To Predict hot-spots or places with a likelihood for crimes 
- To partner with relevant stakeholders in crime prevention

#### Who will be using the results of this project and for making what decisions?
This project can be used by policymakers, Nigerian police force and other security agencies to make effective and informed strategies that can curtail criminal activities and contribute to the nation’s development and also for citizens to know where the criminal activities is taking place in order to take necessary precausions.

Identify atleast 2 collaborators from your organization who will support you by providing


#### Expected Deliverables

#### Mentors (This will be added by ABW Team)

#### References



### The Codes Used for the Project
## GDELT events data
## Documentation: https://data.gdeltproject.org/documentation/GDELT-Data_Format_Codebook.pdf
## Documentation 2: http://data.gdeltproject.org/documentation/CAMEO.Manual.1.1b3.pdf
## Read Data
import pandas as pd
  
pd.options.display.max_rows = 99
pd.options.display.max_columns = 99

%matplotlib inline
%load_ext autoreload
%autoreload 2

## GDELT_DATA_EVENT_CODEBOOK

COLUMN_NAMES = [
"GlobalEventID", # (integer) Globally unique identifier assigned to each event record that uniquely identifies it in the master dataset.
"Date", # (integer) Date the event took place in YYYYMMDD format.
"MonthYear", # (integer) Alternative formatting of the event date, in YYYYMM format.
"Year", #(integer) Alternative formatting of the event date, in YYYY format.
"FractionDate",
    
"Actor1Code", #(character or factor) The complete raw CAMEO code for Actor1 (includes geographic, class, ethnic, religious, and type classes). May be blank if the system was unable to identify an Actor1.
"Actor1Name", #(character) The actual name of the Actor 1. In the case of a political leader or organization, this will be the leader’s formal name (GEORGE W BUSH, UNITED NATIONS), for a geographic match it will be either the country or capital/major city name (UNITED STATES / PARIS), and for ethnic, religious, and type matches it will reflect the root match class (KURD, CATHOLIC, POLICE OFFICER, etc). May be blank if the system was unable to identify an Actor1.
"Actor1CountryCode", #(character or factor) The 3-character CAMEO code for the country affiliation of Actor1. May be blank if the system was unable to identify an Actor1 or determine its country affiliation (such as “UNIDENTIFIED GUNMEN”). Note that through 8/26/2013 matches for South Sudan (“SSD”) may be missing from this field. The country code will be correctly present in the raw CAMEO code in Actor1Code, but may not have been correctly placed into the Actor1CountryCode field – only South Sudan was affected by this issue.
"Actor1KnownGroupCode", # (character or factor) If Actor1 is a known IGO/NGO/rebel organization (United Nations, World Bank, al-Qaeda, etc) with its own CAMEO code, this field will contain that code.
"Actor1EthnicCode", # (character or factor) If the source document specifies the ethnic affiliation of Actor1 and that ethnic group has a CAMEO entry, the CAMEO code is entered here. NOTE: a few special groups like ARAB may also have entries in the type column due to legacy CAMEO behavior. NOTE: this behavior is brand-new and highly experimental and may not capture all affiliations properly.
"Actor1Religion1Code", # (character or factor) If the source document specifies the religious affiliation of Actor1 and that religious group has a CAMEO entry, the CAMEO code is entered here. NOTE: a few special groups like JEW may also have entries in the geographic or type columns due to legacy CAMEO behavior. NOTE: this behavior is brand-new and highly experimental and may not capture all affiliations properly.
"Actor1Religion2Code", # (character or factor) If multiple religious codes are specified for Actor1, this contains the secondary code. Some religion entries automatically use two codes, such as Catholic, which invokes Christianity as Code1 and Catholicism as Code2.
"Actor1Type1Code", # (character or factor) The 3-character CAMEO code of the CAMEO “type” or “role” of Actor1, if specified. This can be a specific role such as Police Forces, Government, Military, Political Opposition, Rebels, etc, a broad role class such as Education, Elites, Media, Refugees, or organizational classes like Non-Governmental Movement. Special codes such as Moderate and Radical may refer to the operational strategy of a group.
"Actor1Type2Code", # (character or factor) If multiple type/role codes are specified for Actor1, this returns the second code.
"Actor1Type3Code", # 
    
"Actor2Code", #(character or factor) The complete raw CAMEO code for Actor1 (includes geographic, class, ethnic, religious, and type classes). May be blank if the system was unable to identify an Actor1.
"Actor2Name", #(character) The actual name of the Actor 1. In the case of a political leader or organization, this will be the leader’s formal name (GEORGE W BUSH, UNITED NATIONS), for a geographic match it will be either the country or capital/major city name (UNITED STATES / PARIS), and for ethnic, religious, and type matches it will reflect the root match class (KURD, CATHOLIC, POLICE OFFICER, etc). May be blank if the system was unable to identify an Actor1.
"Actor2CountryCode", #(character or factor) The 3-character CAMEO code for the country affiliation of Actor1. May be blank if the system was unable to identify an Actor1 or determine its country affiliation (such as “UNIDENTIFIED GUNMEN”). Note that through 8/26/2013 matches for South Sudan (“SSD”) may be missing from this field. The country code will be correctly present in the raw CAMEO code in Actor1Code, but may not have been correctly placed into the Actor1CountryCode field – only South Sudan was affected by this issue.
"Actor2KnownGroupCode", # (character or factor) If Actor1 is a known IGO/NGO/rebel organization (United Nations, World Bank, al-Qaeda, etc) with its own CAMEO code, this field will contain that code.
"Actor2EthnicCode", # (character or factor) If the source document specifies the ethnic affiliation of Actor1 and that ethnic group has a CAMEO entry, the CAMEO code is entered here. NOTE: a few special groups like ARAB may also have entries in the type column due to legacy CAMEO behavior. NOTE: this behavior is brand-new and highly experimental and may not capture all affiliations properly.
"Actor2Religion1Code", # (character or factor) If the source document specifies the religious affiliation of Actor1 and that religious group has a CAMEO entry, the CAMEO code is entered here. NOTE: a few special groups like JEW may also have entries in the geographic or type columns due to legacy CAMEO behavior. NOTE: this behavior is brand-new and highly experimental and may not capture all affiliations properly.
"Actor2Religion2Code", # (character or factor) If multiple religious codes are specified for Actor1, this contains the secondary code. Some religion entries automatically use two codes, such as Catholic, which invokes Christianity as Code1 and Catholicism as Code2.
"Actor2Type1Code", # (character or factor) The 3-character CAMEO code of the CAMEO “type” or “role” of Actor1, if specified. This can be a specific role such as Police Forces, Government, Military, Political Opposition, Rebels, etc, a broad role class such as Education, Elites, Media, Refugees, or organizational classes like Non-Governmental Movement. Special codes such as Moderate and Radical may refer to the operational strategy of a group.
"Actor2Type2Code", # (character or factor) If multiple type/role codes are specified for Actor1, this returns the second code.
"Actor2Type3Code", # 
    
"IsRootEvent", # (logical or binary or byte) The system codes every event found in an entire document, using an array of techniques to deference and link information together. A number of previous projects such as the ICEWS initiative have found that events occurring in the lead paragraph of a document tend to be the most “important.” This flag can therefore be used as a proxy for the rough importance of an event to create subsets of the event stream.
"EventCode", # (character or factor) This is the raw CAMEO action code describing the action that Actor1 performed upon Actor2.
"EventBaseCode", # # (character or factor) CAMEO event codes are defined in a three-level taxonomy. For events at level three in the taxonomy, this yields its level two leaf root node. For example, code “0251” (“Appeal for easing of administrative sanctions”) would yield an EventBaseCode of “025” (“Appeal to yield”). This makes it possible to aggregate events at  various resolutions of specificity. For events at levels two or one, this field will be set to EventCode.
"EventRootCode", # (character or factor) Similar to EventBaseCode, this defines the root-level category the event code falls under. For example, code “0251” (“Appeal for easing of administrative sanctions”) has a root code of “02” (“Appeal”). This makes it possible to aggregate events at various resolutions of specificity. For events at levels two or one, this field will be set to EventCode.
"QuadClass", # (integer) The entire CAMEO event taxonomy is ultimately organized under four primary classifications: Verbal Cooperation, Material Cooperation, Verbal Conflict, and Material Conflict. This field specifies this primary classification for the event type, allowing analysis at the highest level of aggregation. The numeric codes in this field map to the Quad Classes as follows: 1=Verbal Cooperation, 2=Material Cooperation, 3=Verbal Conflict, 4=Material Conflict.
"GoldsteinScale", # (numeric) Each CAMEO event code is assigned a numeric score from -10 to +10, capturing the theoretical potential impact that type of event will have on the stability of a country. This is known as the Goldstein Scale. This field specifies the Goldstein score for each event type. NOTE: this score is based on the type of event, not the specifics of the actual event record being recorded – thus two riots, one with 10 people and one with 10,000, will both receive the same Goldstein score. This can be aggregated to various levels of time resolution to yield an approximation of the stability of a location over time.
"NumMentions", # (integer) This is the total number of mentions of this event across all source documents. Multiple references to an event within a single document also contribute to this count. This can be used as a method of assessing the “importance” of an event: the more discussion of that event, the more likely it is to be significant. The total universe of source documents and the density of events within them vary over time, so it is recommended that this field be normalized by the average or other measure of the universe of events during the time period of interest. NOTE: this field is updated over time if news articles published later discuss this event (for example, in the weeks after a major bombing there will likely be numerous news articles published mentioning the original bombing as context to new developments, while on the one-year anniversary there will likely be further coverage). At this time the daily event stream only includes new event records found each day and does not include these updates; a special “updates” stream will be released in Fall 2013 that will include these.
"NumSources", # (integer) This is the total number of information sources containing one or more mentions of this event. This can be used as a method of assessing the “importance” of an event: the more discussion of that event, the more likely it is to be significant. The total universe of sources varies over time, so it is recommended that this field be normalized by the average or other measure of the universe of events during the time period of interest. NOTE: same as with NumMentions, this field is updated over time to reflect subsequent coverage of the event. Similarly, these updates are not included in the daily event stream, but will be incorporated into a new “updates” stream to be released in Fall 2013.
"NumArticles", # (integer) This is the total number of source documents containing one or more mentions of this event. This can be used as a method of assessing the “importance” of an event: the more discussion of that event, the more likely it is to be significant. The total universe of source documents varies over time, so it is recommended that this field be normalized by the average or other measure of the universe of events during the time period of interest. NOTE: same as with NumMentions, this field is updated over time to reflect subsequent coverage of the event, but these updates are not currently part of the daily event stream.
"AvgTone", # (numeric) This is the average “tone” of all documents containing one or more mentions of this event. The score ranges from -100 (extremely negative) to +100 (extremely positive). Common values range between -10 and +10, with 0 indicating neutral. This can be used as a method of filtering the “context” of events as a subtle measure of the importance of an event and as a proxy for the “impact” of that event. For example, a riot event with a slightly negative average tone is likely to have been a minor occurrence, whereas if it had an extremely negative average tone, it suggests a far more serious occurrence. A riot with a positive score likely suggests a very minor occurrence described in the context of a more positive narrative (such as a report of an attack occurring in a discussion of improving conditions on the ground in a country and how the number of attacks per day has been greatly reduced).

"Actor1Geo_Type", #  (integer) This field specifies the geographic resolution of the match type and holds one of the following values: 1=COUNTRY (match was at the country level), 2=USSTATE (match was to a US state), 3=USCITY (match was to a US city or landmark), 4=WORLDCITY (match was to a city or landmark outside the US), 5=WORLDSTATE (match was to an Administrative Division 1 outside the US – roughly equivalent to a US state). This can be used to filter events by geographic specificity, for example, extracting only those events with a landmark-level geographic resolution for mapping. Note that matches with codes 1 (COUNTRY), 2 (USSTATE), and 5 (WORLDSTATE) will still provide a latitude/longitude pair, which will be the centroid of that country or state, but the FeatureID field below will be blank.
"Actor1Geo_Fullname", #  (character) This is the full human-readable name of the matched location. In the case of a country it is simply the country name. For US and World states it is in the format of “State, Country Name”, while for all other matches it is in the format of “City/Landmark, State, Country”. This can be used to label locations when placing events on a map. NOTE: this field reflects the precise name used to refer to the location in the text itself, meaning it may contain multiple spellings of the same location – use the FeatureID column to determine whether two location names refer to the same place.
"Actor1Geo_CountryCode", #  (character) This is the 2-character FIPS10-4 country code for the location.
"Actor1Geo_ADM1Code", #  (character) This is the 2-character FIPS10-4 country code followed by the 2-character FIPS10-4 administrative division 1 (ADM1) code for the administrative division housing the landmark. In the case of the United States, this is the 2-character shortform of the state’s name (such as “TX” for Texas).
"Actor1Geo_Lat", #  (numeric) This is the centroid latitude of the landmark for mapping.
"Actor1Geo_Long", #  (numeric) This is the centroid longitude of the landmark for mapping.
"Actor1Geo_FeatureID", #  (signed integer) This is the GNS or GNIS FeatureID for this location. More information on these values can be found in Leetaru (2012). 5 NOTE: This field will be blank except when Actor1Geo_Type has a value of 3 or 4. A small percentage of small cities andtowns may have a blank value in this field even for Actor1Geo_Type values of 3 or 4: this will be corrected in the 2.0 release of GDELT. N

    
"Actor2Geo_Type", #  (integer) This field specifies the geographic resolution of the match type and holds one of the following values: 1=COUNTRY (match was at the country level), 2=USSTATE (match was to a US state), 3=USCITY (match was to a US city or landmark), 4=WORLDCITY (match was to a city or landmark outside the US), 5=WORLDSTATE (match was to an Administrative Division 1 outside the US – roughly equivalent to a US state). This can be used to filter events by geographic specificity, for example, extracting only those events with a landmark-level geographic resolution for mapping. Note that matches with codes 1 (COUNTRY), 2 (USSTATE), and 5 (WORLDSTATE) will still provide a latitude/longitude pair, which will be the centroid of that country or state, but the FeatureID field below will be blank.
"Actor2Geo_Fullname", #  (character) This is the full human-readable name of the matched location. In the case of a country it is simply the country name. For US and World states it is in the format of “State, Country Name”, while for all other matches it is in the format of “City/Landmark, State, Country”. This can be used to label locations when placing events on a map. NOTE: this field reflects the precise name used to refer to the location in the text itself, meaning it may contain multiple spellings of the same location – use the FeatureID column to determine whether two location names refer to the same place.
"Actor2Geo_CountryCode", #  (character) This is the 2-character FIPS10-4 country code for the location.
"Actor2Geo_ADM1Code", #  (character) This is the 2-character FIPS10-4 country code followed by the 2-character FIPS10-4 administrative division 1 (ADM1) code for the administrative division housing the landmark. In the case of the United States, this is the 2-character shortform of the state’s name (such as “TX” for Texas).
"Actor2Geo_Lat", #  (numeric) This is the centroid latitude of the landmark for mapping.
"Actor2Geo_Long", #  (numeric) This is the centroid longitude of the landmark for mapping.
"Actor2Geo_FeatureID", #  (signed integer) This is the GNS or GNIS FeatureID for this location. More information on these values can be found in Leetaru (2012). 5 NOTE: This field will be blank except when Actor1Geo_Type has a value of 3 or 4. A small percentage of small cities andtowns may have a blank value in this field even for Actor1Geo_Type values of 3 or 4: this will be corrected in the 2.0 release of GDELT. N

"ActionGeo_Type", #  (integer) This field specifies the geographic resolution of the match type and holds one of the following values: 1=COUNTRY (match was at the country level), 2=USSTATE (match was to a US state), 3=USCITY (match was to a US city or landmark), 4=WORLDCITY (match was to a city or landmark outside the US), 5=WORLDSTATE (match was to an Administrative Division 1 outside the US – roughly equivalent to a US state). This can be used to filter events by geographic specificity, for example, extracting only those events with a landmark-level geographic resolution for mapping. Note that matches with codes 1 (COUNTRY), 2 (USSTATE), and 5 (WORLDSTATE) will still provide a latitude/longitude pair, which will be the centroid of that country or state, but the FeatureID field below will be blank.
"ActionGeo_Fullname", #  (character) This is the full human-readable name of the matched location. In the case of a country it is simply the country name. For US and World states it is in the format of “State, Country Name”, while for all other matches it is in the format of “City/Landmark, State, Country”. This can be used to label locations when placing events on a map. NOTE: this field reflects the precise name used to refer to the location in the text itself, meaning it may contain multiple spellings of the same location – use the FeatureID column to determine whether two location names refer to the same place.
"ActionGeo_CountryCode", #  (character) This is the 2-character FIPS10-4 country code for the location.
"ActionGeo_ADM1Code", #  (character) This is the 2-character FIPS10-4 country code followed by the 2-character FIPS10-4 administrative division 1 (ADM1) code for the administrative division housing the landmark. In the case of the United States, this is the 2-character shortform of the state’s name (such as “TX” for Texas).
"ActionGeo_Lat", #  (numeric) This is the centroid latitude of the landmark for mapping.
"ActionGeo_Long", #  (numeric) This is the centroid longitude of the landmark for mapping.
"ActionGeo_FeatureID", #  (signed integer) This is the GNS or GNIS FeatureID for this location. More information on these values can be found in Leetaru (2012). 5 NOTE: This field will be blank except when Actor1Geo_Type has a value of 3 or 4. A small percentage of small cities andtowns may have a blank value in this field even for Actor1Geo_Type values of 3 or 4: this will be corrected in the 2.0 release of GDELT. N

"DATEADDED", # (integer) This field stores the date the event was added to the master database.
"SOURCEURL", #  (character) This field is only present in the daily event stream files beginning April 1, 2013 and lists the URL of the news article the event was found in. If the event was found in an article from the BBC Monitoring service, this field will contain “BBC Monitoring.” If an event was mentioned in multiple articles, only one of the URLs is provided.
]

## event_Codes_with_Event_Codes_Name

EVENT_CODES = [
"01:", # MAKE PUBLIC STATEMENT
"010:", # Make statement, not specified below
"011:", #  Decline comment
"012:", # Make pessimistic comment
"013:", # Make optimistic comment
"014: ", #Consider policy option
"015:", # Acknowledge or claim responsibility
"016:", # Deny responsibility
"017:", # Engage in symbolic act
"018:", # Make empathetic comment
"019:", # Express accord

"02:", # APPEAL
"020:", # Make an appeal or request, not specified below
"021: ", #Appeal for material cooperation, not specified below
"0211:", # Appeal for economic cooperation
"0212: ", #Appeal for military cooperation
"0213: ", #Appeal for judicial cooperation
"0214:", # Appeal for intelligence
"022:", # Appeal for diplomatic cooperation (such as policy support)
"023: ", #Appeal for aid, not specified below
"0231:", # Appeal for economic aid
"0232:", # Appeal for military aid
"0233:", # Appeal for humanitarian aid
"0234:", # Appeal for military protection or peacekeeping
"024: ", # Appeal for political reform, not specified below
"0241:", # Appeal for change in leadership
"0242: ", # Appeal for policy change
"0243:", # Appeal for rights
"0244:", # Appeal for change in institutions, regime
"025: ", # Appeal to yield, not specified below
"0251:", # Appeal for easing of administrative sanctions
"0252:", # Appeal for easing of political dissent
"0253:", # Appeal for release of persons or property
"0254:", # Appeal for easing of economic sanctions, boycott, or embargo
"0255:", # Appeal for target to allow international involvement (non-mediation)
"0256:", # Appeal for de-escalation of military engagement
"026:", # Appeal to others to meet or negotiate
"027:", # Appeal to others to settle dispute
"028:", # Appeal to engage in or accept mediation

"03:", # EXPRESS INTENT TO COOPERATE
"030:", # Express intent to cooperate, not specified below
"031:", # Express intent to engage in material cooperation, not specified below
"0311:", # Express intent to cooperate economically
"0312:", # Express intent to cooperate militarily
"0313:", # Express intent to cooperate on judicial matters
"0314:", # Express intent to cooperate on intelligence
"032:", # Express intent to engage in diplomatic cooperation (such as policy support)
"033:", # Express intent to provide material aid, not specified below
"0331:", # Express intent to provide economic aid
"0332:", # Express intent to provide military aid
"0333:", # Express intent to provide humanitarian aid
"0334:", # Express intent to provide military protection or peacekeeping
"034:", # Express intent to institute political reform, not specified below
"0341:", # Express intent to change leadership
"0342:", # Express intent to change policy
"0343:", # Express intent to provide rights
"0344:", # Express intent to change institutions, regime
"035:", # Express intent to yield, not specified below
"0351:", # Express intent to ease administrative sanctions
"0352:", # Express intent to ease popular dissent
"0353:", # Express intent to release persons or property
"0354:", # Express intent to ease economic sanctions, boycott, or embargo
"0355:", # Express intent to allow international involvement (non-mediation)
"0356:", # Express intent to de-escalate military engagement
"036:", # Express intent to meet or negotiate
"037:", # Express intent to settle dispute
"038:", # Express intent to accept mediation
"039:", # Express intent to mediate

"04:", # CONSULT
"040:", # Consult, not specified below
"041:", # Discuss by telephone
"042:", # Make a visit
"043:", # Host a visit
"044:", # Meet at a ”third” location
"045:", # Mediate
"046:", # Engage in negotiation

"05:", # ENGAGE IN DIPLOMATIC COOPERATION
"050:", # Engage in diplomatic cooperation, not specified below
"051:", # Praise or endorse
"052:", # Defend verbally
"053:", # Rally support on behalf of
"054:", # Grant diplomatic recognition
"055:", # Apologize
"056:", # Forgive
"057:", # Sign formal agreement

"06:", # ENGAGE IN MATERIAL COOPERATION
"060:", # Engage in material cooperation, not specified below
"061:", # Cooperate economically
"062:", # Cooperate militarily
"063:", # Engage in judicial cooperation
"064:", # Share intelligence or information

"07:", # PROVIDE AID
"070:", # Provide aid, not specified below
"071:", # Provide economic aid
"072:", # Provide military aid
"073:", # Provide humanitarian aid
"074:", # Provide military protection or peacekeeping
"075:", # Grant asylum

"08:", # YIELD
"080:", # Yield, not specified below
"081:", # Ease administrative sanctions, not specified below
"0811:", # Ease restrictions on political freedoms
"0812:", # Ease ban on political parties or politicians
"0813:", # Ease curfew
"0814:", # Ease state of emergency or martial law
"082:", # Ease political dissent
"083:", # Accede to requests or demands for political reform, not specified below
"0831:", # Accede to demands for change in leadership
"0832:", # Accede to demands for change in policy
"0833:", # Accede to demands for rights
"0834:", # Accede to demands for change in institutions, regime
"084:", # Return, release, not specified below
"0841:", # Return, release person(s)
"0842:", # Return, release property
"085:", # Ease economic sanctions, boycott, embargo
"086:", # Allow international involvement, not specified below
"0861:", # Receive deployment of peacekeepers
"0862:", # Receive inspectors
"0863:", # Allow humanitarian access
"087:", # De-escalate military engagement
"0871:", # Declare truce, ceasefire
"0872:", # Ease military blockade
"0873:", # Demobilize armed forces
"0874:", # Retreat or surrender militarily

"09:", # INVESTIGATE
"090:", # Investigate, not specified below
"091:", # Investigate crime, corruption
"092:", # Investigate human rights abuses
"093:", # Investigate military action
"094:", # Investigate war crimes

"10:", # DEMAND
"100:", # Demand, not specified below
"101:", # Demand material cooperation, not specified below
"1011:", # Demand economic cooperation
"1012:", # Demand military cooperation
"1013:", # Demand judicial cooperation
"1014:", # Demand intelligence cooperation
"102:", # Demand diplomatic cooperation (such as policy support)
"103:", # Demand material aid, not specified below
"1031:", # Demand economic aid
"1032:", # Demand military aid
"1033:", # Demand humanitarian aid
"1034:", # Demand military protection or peacekeeping
"104:", # Demand political reform, not specified below
"1041:", # Demand change in leadership
"1042:", # Demand policy change
"1043:", # Demand rights
"1044:", # Demand change in institutions, regime
"105:", # Demand that target yields, not specified below
"1051:", # Demand easing of administrative sanctions
"1052:", # Demand easing of political dissent
"1053:", # Demand release of persons or property
"1054:", # Demand easing of economic sanctions, boycott, or embargo
"1055:", # Demand that target allows international involvement (non-mediation)
"1056:", # Demand de-escalation of military engagement
"106:", # Demand meeting, negotiation
"107:", # Demand settling of dispute
"108:", # Demand mediation

"11:", # DISAPPROVE
"110:", # Disapprove, not specified below
"111:", # Criticize or denounce
"112:", # Accuse, not specified below
"1121:", # Accuse of crime, corruption
"1122:", # Accuse of human rights abuses
"1123:", # Accuse of aggression
"1124:", # Accuse of war crimes
"1125:", # Accuse of espionage, treason
"113:", # Rally opposition against
"114:", # Complain officially
"115:", # Bring lawsuit against
"116:", # Find guilty or liable (legally)

"12:", # REJECT
"120:", # Reject, not specified below
"121:", # Reject material cooperation
"1211:", # Reject economic cooperation
"1212:", # Reject military cooperation
"122:", # Reject request or demand for material aid, not specified below
"1221:", # Reject request for economic aid
"1222:", # Reject request for military aid
"1223:", # Reject request for humanitarian aid
"1224:", # Reject request for military protection or peacekeeping
"123:", # Reject request or demand for political reform, not specified below
"1231:", # Reject request for change in leadership
"1232:", # Reject request for policy change
"1233:", # Reject request for rights
"1234:", # Reject request for change in institutions, regime
"124:", # Refuse to yield, not specified below
"1241:", # Refuse to ease administrative sanctions
"1242:", # Refuse to ease popular dissent
"1243:", # Refuse to release persons or property
"1244:", # Refuse to ease economic sanctions, boycott, or embargo
"1245:", # Refuse to allow international involvement (non mediation)
"1246:", # Refuse to de-escalate military engagement
"125:", # Reject proposal to meet, discuss, or negotiate
"126:", # Reject mediation
"127:", # Reject plan, agreement to settle dispute
"128:", # Defy norms, law
"129:", # Veto

"13:", # THREATEN
"130:", # Threaten, not specified below
"131:", # Threaten non-force, not specified below
"1311:", # Threaten to reduce or stop aid
"1312:", # Threaten with sanctions, boycott, embargo
"1313:", # Threaten to reduce or break relations
"132:", # Threaten with administrative sanctions, not specified below
"1321:", # Threaten with restrictions on political freedoms
"1322:", # Threaten to ban political parties or politicians
"1323:", # Threaten to impose curfew
"1324:", # Threaten to impose state of emergency or martial law
"133:", # Threaten with political dissent, protest
"134:", # Threaten to halt negotiations
"135:", # Threaten to halt mediation
"136:", # Threaten to halt international involvement (non-mediation)
"137:", # Threaten with repression
"138:", # Threaten with military force, not specified below
"1381:", # Threaten blockade
"1382:", # Threaten occupation
"1383:", # Threaten unconventional violence
"1384:", # Threaten conventional attack
"1385:", # Threaten attack with WMD
"139:", # Give ultimatum

"14:", # PROTEST
"140:", # Engage in political dissent, not specified below
"141:", # Demonstrate or rally, not specified below
"1411:", # Demonstrate for leadership change
"1412:", # Demonstrate for policy change
"1413:", # Demonstrate for rights
"1414:", # Demonstrate for change in institutions, regime
"142:", # Conduct hunger strike, not specified below
"1421", #: Conduct hunger strike for leadership change
"1422:", # Conduct hunger strike for policy change
"1423:", # Conduct hunger strike for rights
"1424:", # Conduct hunger strike for change in institutions, regime
"143:", # Conduct strike or boycott, not specified below
"1431:", # Conduct strike or boycott for leadership change
"1432:", # Conduct strike or boycott for policy change
"1433:", # Conduct strike or boycott for rights
"1434:", # Conduct strike or boycott for change in institutions, regime
"144:", # Obstruct passage, block, not specified below
"1441:", # Obstruct passage to demand leadership change
"1442:", # Obstruct passage to demand policy change
"1443:", # Obstruct passage to demand rights
"1444:", # Obstruct passage to demand change in institutions, regime
"145:", # Protest violently, riot, not specified below
"1451:", # Engage in violent protest for leadership change
"1452:", # Engage in violent protest for policy change
"1453:", # Engage in violent protest for rights
"1454:", # Engage in violent protest for change in institutions, regime

"15:", # EXHIBIT FORCE POSTURE
"150:", # Demonstrate military or police power, not specified below
"151:", # Increase police alert status
"152:", # Increase military alert status
"153:", # Mobilize or increase police power
"154:", # Mobilize or increase armed forces
"155:", # Mobilize or increase cyber-forces
"16:", # REDUCE RELATIONS
"160:", # Reduce relations, not specified below
"161:", # Reduce or break diplomatic relations
"162:", # Reduce or stop material aid, not specified below
"1621:", # Reduce or stop economic assistance
"1622:", # Reduce or stop military assistance
"1623:", # Reduce or stop humanitarian assistance
"163:", # Impose embargo, boycott, or sanctions
"164:", # Halt negotiations
"165:", # Halt mediation
"166:", # Expel or withdraw, not specified below
"1661:", # Expel or withdraw peacekeepers
"1662:", # Expel or withdraw inspectors, observers
"1663:", # Expel or withdraw aid agencies

"17:", # COERCE
"170:", # Coerce, not specified below
"171:", # Seize or damage property, not specified below
"1711:", # Confiscate property
"1712:", # Destroy property
"172:", # Impose administrative sanctions, not specified below
"1721:", # Impose restrictions on political freedoms
"1722:", # Ban political parties or politicians
"1723:", # Impose curfew
"1724:", # Impose state of emergency or martial law
"173:", # Arrest, detain, or charge with legal action
"174:", # Expel or deport individuals
"175:", # Use tactics of violent repression
"176:", # Attack cybernetically

"18:", # ASSAULT
"180:", # Use unconventional violence, not specified below
"181:", # Abduct, hijack, or take hostage
"182:", # Physically assault, not specified below
"1821:", # Sexually assault
"1822:", # Torture
"1823:", # Kill by physical assault
"183:", # Conduct suicide, car, or other non-military bombing, not specified below
"1831:", # Carry out suicide bombing
"1832:", # Carry out vehicular bombing
"1833:", # Carry out roadside bombing
"1834:", # Carry out location bombing
"184:", # Use as human shield
"185:", # Attempt to assassinate
"186:", # Assassinate

"19:", # FIGHT
"190:", # Use conventional military force, not specified below
"191:", # Impose blockade, restrict movement
"192:", # Occupy territory
"193:", # Fight with small arms and light weapons
"194:", # Fight with artillery and tanks
"195:", # Employ aerial weapons, not specified below
"1951:", # Employ precision-guided aerial munitions
"1952:", # Employ remotely piloted aerial munitions
"196:", # Violate ceasefire

"20:", # USE UNCONVENTIONAL MASS VIOLENCE
"200:", # Use unconventional mass violence, not specified below
"201:", # Engage in mass expulsion
"202:", # Engage in mass killings
"203:", # Engage in ethnic cleansing
"204:", # Use weapons of mass destruction, not specified below
"2041:", # Use chemical, biological, or radiological weapons
"2042:", # Detonate nuclear weapons
]

## Actor_Names_with_Codes

ACTOR_NAMES = [
"NGA", # Nigeria
"NGAABI", # Abia (Nigeria) 
"NGAABU", # Abuja (Nigeria) 
"NGAADA", # Adamawa (Nigeria) 
"NGAAKI", # Akwa Ibom (Nigeria) 
"NGAANB", # Anambra (Nigeria) 
"NGABAU", # Bauchi (Nigeria) 
"NGABAY", # Bayelsa (Nigeria) 
"NGABIA", # Biafra (Nigeria)
"NGABNU", # Benue (Nigeria) 
"NGABOR", # Borno (Nigeria) 
"NGACRR", # Cross River (Nigeria) 
"NGADEL", # Delta (Nigeria) 
"NGAEBO", # Edo (Nigeria) 
"NGAEKI", # Ekiti (Nigeria) 
"NGAENU", # Enugu (Nigeria) 
"NGAGOM", # Gombe (Nigeria) 
"NGAHAU", # Hausa (ethnic group) 
"NGAIBO", # Ibo, Igbo (ethnic group) 
"NGAIJW", # Ijaws (ethnic group) 
"NGAIMO", # Imo (Nigeria) 
"NGAJIG", # Jigawa (Nigeria) 
"NGAKAD", # Kaduna (Nigeria) 
"NGAKAN", # Kano (Nigeria) 
"NGAKAT", # Katsina (Nigeria) 
"NGAKEB", # Kebbi (Nigeria) 
"NGAKOG", # Kogi (Nigeria) 
"NGAKWA", # Kwara (Nigeria) 
"NGALAG",# Lagos (Nigeria) 
"NGANAS", # Nassarawa (Nigeria) 
"NGANDR", # Niger Delta Region (Nigeria) 
"NGANGR", # Niger (Nigeria) 
"NGANNG", # North Nigeria (Nigeria) 
"NGAOGO", # Ogoni (ethnic group) 
"NGAOGU", # Ogun (Nigeria) 
"NGAOND", # Ondo (Nigeria)
"NGAOSU", # Osun (Nigeria) 
"NGAOYO", # Oyo (Nigeria) 
"NGAPLA", # Plateu State (Nigeria) 
"NGARIV", # Rivers (Nigeria) 
"NGASOK", # Sokoto (Nigeria) 
"NGATAR", # Taraba (Nigeria) 
"NGATIV", # Tiv (ethnic group, language) 
"NGAYOB", # Yobe (Nigeria) 
"NGAYRB", # Yoruba (ethnic group) 
"NGAZAM", # Zamfara (Nigeria)
]

## Ethnic_Group_with_Codes

ETHNIC_GROUP_CODES = [
    "ful", # Fula (Fulani)
    "hau", # Hausa (Hausa-Fulani)
    "ibo", # Igbo
    "ijo", # Ijaw
    "yor", # Yoruba
]

## Read from Drive

from google.colab import drive
drive.mount('/content/drive')

## Importing a 1st Day Data

DATE = "20210106"
filename = "/content/drive/MyDrive/" + DATE + ".export.CSV.zip"

df = pd.read_csv(filename, sep='\t', names=COLUMN_NAMES)

## Shape of the Data from Data Frame

df.shape

## How to get the Headings of the Data Frame

df.head()

## How to Filter Nigeria data and the Column to Select

filter_nigeria = df["Actor1CountryCode"] == "NGA"

df = df[filter_nigeria]

df

## How to Query the selected EventCode interested in filtering

   df.query('EventCode in [84, 841, 87, 874, 90, 91, 130, 1383, 1385, 1711, 1712, 173, 176, 180, 181, 182, 1821, 1822, 1823, 183, 1831, 1832, 1833, 1834, 185, 186, 190, 191, 193, 194, 195, 202, 203, 204]')
   
## How to Stored a Filtered Events into New folder in a google drive

filename = "/content/drive/MyDrive/Output2/" + DATE + "_NG_crime.csv"

df.to_csv(filename, index=False)

## How to Combine the steps (reading a file, filtering and saving the filtered file) into a single function

def filter_df(date):

  filename = "/content/drive/MyDrive/" + date + ".export.CSV.zip"

  df = pd.read_csv(filename, sep='\t', names=COLUMN_NAMES)
  filter_nigeria = df["Actor1CountryCode"] == "NGA"

  df = df[filter_nigeria]
  df = df.query('EventCode in [84, 841, 87, 874, 90, 91, 130, 1383, 1385, 1711, 1712, 173, 176, 180, 181, 182, 1821, 1822, 1823, 183, 1831, 1832, 1833, 1834, 185, 186, 190, 191, 193, 194, 195, 202, 203, 204]')
  filename = "/content/drive/MyDrive/Output2/" + date + "_NG_crime.csv"

  df.to_csv(filename, index=False)
  
  ## Filter a day to make sure your above code is stored
  
  filter_df("20210102")
  
  ## Make a list of all the dates (files) you want to use
  
  FILES = ["20210101", "20210102", "20210103", "20210104", "20210105", "20210106", "20210107", "20210108", "20210109", "20210110", "20210111", "20210112", "20210113", "20210114", "20210115", "20210116", "20210117", "20210118", "20210119", "20210120", "20210121", "20210122", "20210123", "20210124", "20210125", "20210126", "20210127", "20210128", "20210129", "20210130", "20210131", "20210201", "20210202", "20210203", "20210204", "20210205", "20210206", "20210207", "20210208", "20210209", "20210210", "20210211", "20210212", "20210213", "20210214", "20210215", "20210216", "20210217", "20210218", "20210219", "20210220", "20210221", "20210222", "20210223", "20210224", "20210225", "20210226", "20210227", "20210228", "20210301", "20210302", "20210303", "20210304", "20210305", "20210306", "20210307", "20210308", "20210309", "20210310", "20210311", "20210312", "20210313", "20210314", "20210315", "20210316", "20210317", "20210318", "20210319", "20210320", "20210321", "20210322", "20210323", "20210324", "20210325", "20210326", "20210327", "20210328", "20210329", "20210330", "20210331", "20210401", "20210402", "20210403", "20210405", "20210406", "20210407", "20210408", "20210409", "20210410", "20210411", "20210412", "20210413", "20210414", "20210415", "20210416", "20210417", "20210418", "20210419", "20210420", "20210421", "20210422", "20210423", "20210424", "20210425", "20210426", "20210427", "20210428", "20210429", "20210430", "20210501", "20210502", "20210503", "20210504", "20210505", "20210506", "20210507", "20210508", "20210509", "20210510", "20210511", "20210512", "20210513", "20210514", "20210515", "20210516", "20210517", "20210518", "20210519", "20210520", "20210521", "20210522", "20210523", "20210524", "20210525", "20210526", "20210527", "20210528", "20210529", "20210530", "20210531", "20210601", "20210602", "20210603", "20210604", "20210605", "20210606", "20210607", "20210608", "20210609", "20210610", "20210611", "20210612", "20210613", "20210614", "20210615", "20210616", "20210617", "20210618", "20210619", "20210620", "20210621", "20210622", "20210623", "20210624", "20210625", "20210626", "20210627", "20210628", "20210629", "20210630", "20210601", "20210701", "20210702", "20210703", "20210704", "20210705", "20210706", "20210707", "20210708", "20210709", "20210710", "20210711", "20210712", "20210713", "20210714", "20210715", "20210716", "20210717", "20210718", "20210719", "20210720", "20210721", "20210722", "20210723", "20210724", "20210725", "20210726", "20210727", "20210728", "20210729", "20210730", "20210731", "20210801", "20210802", "20210803", "20210804", "20210805", "20210806", "20210807", "20210808", "20210809", "20210810", "20210811", "20210812", "20210813", "20210814", "20210815", "20210816", "20210817", "20210818", "20210819", "20210820", "20210821", "20210822", "20210823", "20210824", "20210825", "20210826", "20210827", "20210828", "20210829", "20210830", "20210831", "20210901", "20210902", "20210903", "20210904", "20210905", "20210906", "20210907", "20210908", "20210909", "20210910", "20210911", "20210912", "20210913", "20210914", "20210915", "20210916", "20210917", "20210918", "20210919", "20210920", "20210921", "20210922", "20210923", "20210924", "20210925", "20210926", "20210927", "20210928", "20210929", "20210930", "20211001", "20211002", "20211003", "20211004", "20211005", "20211006", "20211007", "20211008", "20211009", "20211010", "20211011", "20211012", "20211013", "20211014", "20211015", "20211016", "20211017", "20211018", "20211019", "20211020", "20211021", "20211022", "20211023", "20211024", "20211025", "20211026", "20211027", "20211028", "20211029", "20211030", "20211031", "20211101", "20211102", "20211103", "20211104", "20211105", "20211106", "20211107", "20211108", "20211109", "20211110", "20211111", "20211112", "20211113", "20211114", "20211115", "20211116", "20211117", "20211118", "20211119", "20211120", "20211121", "20211122", "20211123", "20211124", "20211125", "20211126", "20211127", "20211128", "20211129","20211130", "20211201", "20211202", "20211203", "20211204", "20211205", "20211206", "20211207", "20211208", "20211209", "20211210", "20211211", "20211212", "20211213", "20211214", "20211215", "20211216", "20211217", "20211218", "20211219", "20211220", "20211221", "20211222", "20211223", "20211224", "20211225", "20211226", "20211227", "20211228", "20211229", "20211230", "20211231", "20220101", "20220102", "20220103", "20220104", "20220105", "20220106", "20220107", "20220108", "20220109", "20220110", "20220111", "20220112", "20220113", "20220114", "20220115", "20220116", "20220117", "20220118", "20220119", "20220120", "20220121", "20220122", "20220123", "20220124", "20220125", "20220126", "20220127", "20220128", "20220129", "20220130", "20220131", "20220201", "20220202", "20220203", "20220204", "20220205", "20220206", "20220207", "20220208", "20220209", "20220210", "20220211", "20220212", "20220213", "20220214", "20220215", "20220216", "20220217", "20220218", "20220219", "20220220", "20220221", "20220222", "20220223", "20220224", "20220225", "20220226", "20220227", "20220228", "20220301","20220302", "20220303", "20220304", "20220305", "20220306", "20220307", "20220308", "20220309", "20220310", "20220311", "20220312", "20220313", "20220314", "20220315", "20220316", "20220317", "20220318", "20220319", "20220320", "20220321", "20220322", "20220323", "20220324", "20220325", "20220326", "20220327", "20220328", "20220329", "20220330", "20220331", "20220401", "20220402", "20220403", "20220405", "20220406", "20220407", "20220408", "20220409", "20220410", "20220411", "20220412", "20220413", "20220414", "20220415", "20220416", "20220417", "20220418", "20220419", "20220420", "20220421", "20220422", "20220423", "20220424", "20220425", "20220426", "20220427", "20220428", "20220429", "20220430", "20220501", "20220502", "20220503", "20220504", "20220505", "20220506", "20220507", "20220508", "20220509", "20220510", "20220511", "20220512", "20220513", "20220514", "20220515", "20220516", "20220517", "20220518", "20220519", "20220520", "20220521", "20220522", "20220523", "20220524", "20220525", "20220526", "20220527", "20220528", "20220529"]
  
  ## Use a for loop to call the function to all files in the list
  
  for file in FILES:
  filter_df(file)
  print(file)
  
  ## You can open a new notebook to import pandas
  
  import pandas as pd
  
pd.options.display.max_rows = 99
pd.options.display.max_columns = 99

%matplotlib inline
%load_ext autoreload
%autoreload 2

## Mount drive again

from google.colab import drive
drive.mount('/content/drive')

## List of the dates

FILES = ["20210101", "20210102", "20210103", "20210104", "20210105", "20210106", "20210107", "20210108", "20210109", "20210110", "20210111", "20210112", "20210113", "20210114", "20210115", "20210116", "20210117", "20210118", "20210119", "20210120", "20210121", "20210122", "20210123", "20210124", "20210125", "20210126", "20210127", "20210128", "20210129", "20210130", "20210131", "20210201", "20210202", "20210203", "20210204", "20210205", "20210206", "20210207", "20210208", "20210209", "20210210", "20210211", "20210212", "20210213", "20210214", "20210215", "20210216", "20210217", "20210218", "20210219", "20210220", "20210221", "20210222", "20210223", "20210224", "20210225", "20210226", "20210227", "20210228", "20210301", "20210302", "20210303", "20210304", "20210305", "20210306", "20210307", "20210308", "20210309", "20210310", "20210311", "20210312", "20210313", "20210314", "20210315", "20210316", "20210317", "20210318", "20210319", "20210320", "20210321", "20210322", "20210323", "20210324", "20210325", "20210326", "20210327", "20210328", "20210329", "20210330", "20210331", "20210401", "20210402", "20210403", "20210405", "20210406", "20210407", "20210408", "20210409", "20210410", "20210411", "20210412", "20210413", "20210414", "20210415", "20210416", "20210417", "20210418", "20210419", "20210420", "20210421", "20210422", "20210423", "20210424", "20210425", "20210426", "20210427", "20210428", "20210429", "20210430", "20210501", "20210502", "20210503", "20210504", "20210505", "20210506", "20210507", "20210508", "20210509", "20210510", "20210511", "20210512", "20210513", "20210514", "20210515", "20210516", "20210517", "20210518", "20210519", "20210520", "20210521", "20210522", "20210523", "20210524", "20210525", "20210526", "20210527", "20210528", "20210529", "20210530", "20210531", "20210601", "20210602", "20210603", "20210604", "20210605", "20210606", "20210607", "20210608", "20210609", "20210610", "20210611", "20210612", "20210613", "20210614", "20210615", "20210616", "20210617", "20210618", "20210619", "20210620", "20210621", "20210622", "20210623", "20210624", "20210625", "20210626", "20210627", "20210628", "20210629", "20210630", "20210601", "20210701", "20210702", "20210703", "20210704", "20210705", "20210706", "20210707", "20210708", "20210709", "20210710", "20210711", "20210712", "20210713", "20210714", "20210715", "20210716", "20210717", "20210718", "20210719", "20210720", "20210721", "20210722", "20210723", "20210724", "20210725", "20210726", "20210727", "20210728", "20210729", "20210730", "20210731", "20210801", "20210802", "20210803", "20210804", "20210805", "20210806", "20210807", "20210808", "20210809", "20210810", "20210811", "20210812", "20210813", "20210814", "20210815", "20210816", "20210817", "20210818", "20210819", "20210820", "20210821", "20210822", "20210823", "20210824", "20210825", "20210826", "20210827", "20210828", "20210829", "20210830", "20210831", "20210901", "20210902", "20210903", "20210904", "20210905", "20210906", "20210907", "20210908", "20210909", "20210910", "20210911", "20210912", "20210913", "20210914", "20210915", "20210916", "20210917", "20210918", "20210919", "20210920", "20210921", "20210922", "20210923", "20210924", "20210925", "20210926", "20210927", "20210928", "20210929", "20210930", "20211001", "20211002", "20211003", "20211004", "20211005", "20211006", "20211007", "20211008", "20211009", "20211010", "20211011", "20211012", "20211013", "20211014", "20211015", "20211016", "20211017", "20211018", "20211019", "20211020", "20211021", "20211022", "20211023", "20211024", "20211025", "20211026", "20211027", "20211028", "20211029", "20211030", "20211031", "20211101", "20211102", "20211103", "20211104", "20211105", "20211106", "20211107", "20211108", "20211109", "20211110", "20211111", "20211112", "20211113", "20211114", "20211115", "20211116", "20211117", "20211118", "20211119", "20211120", "20211121", "20211122", "20211123", "20211124", "20211125", "20211126", "20211127", "20211128", "20211129","20211130", "20211201", "20211202", "20211203", "20211204", "20211205", "20211206", "20211207", "20211208", "20211209", "20211210", "20211211", "20211212", "20211213", "20211214", "20211215", "20211216", "20211217", "20211218", "20211219", "20211220", "20211221", "20211222", "20211223", "20211224", "20211225", "20211226", "20211227", "20211228", "20211229", "20211230", "20211231", "20220101", "20220102", "20220103", "20220104", "20220105", "20220106", "20220107", "20220108", "20220109", "20220110", "20220111", "20220112", "20220113", "20220114", "20220115", "20220116", "20220117", "20220118", "20220119", "20220120", "20220121", "20220122", "20220123", "20220124", "20220125", "20220126", "20220127", "20220128", "20220129", "20220130", "20220131", "20220201", "20220202", "20220203", "20220204", "20220205", "20220206", "20220207", "20220208", "20220209", "20220210", "20220211", "20220212", "20220213", "20220214", "20220215", "20220216", "20220217", "20220218", "20220219", "20220220", "20220221", "20220222", "20220223", "20220224", "20220225", "20220226", "20220227", "20220228", "20220301","20220302", "20220303", "20220304", "20220305", "20220306", "20220307", "20220308", "20220309", "20220310", "20220311", "20220312", "20220313", "20220314", "20220315", "20220316", "20220317", "20220318", "20220319", "20220320", "20220321", "20220322", "20220323", "20220324", "20220325", "20220326", "20220327", "20220328", "20220329", "20220330", "20220331", "20220401", "20220402", "20220403", "20220405", "20220406", "20220407", "20220408", "20220409", "20220410", "20220411", "20220412", "20220413", "20220414", "20220415", "20220416", "20220417", "20220418", "20220419", "20220420", "20220421", "20220422", "20220423", "20220424", "20220425", "20220426", "20220427", "20220428", "20220429", "20220430", "20220501", "20220502", "20220503", "20220504", "20220505", "20220506", "20220507", "20220508", "20220509", "20220510", "20220511", "20220512", "20220513", "20220514", "20220515", "20220516", "20220517", "20220518", "20220519", "20220520", "20220521", "20220522", "20220523", "20220524", "20220525", "20220526", "20220527", "20220528", "20220529"]

## Call the dates stored in the files 
data = []
for file in FILES:
  filename = "/content/drive/MyDrive/Output2/" + file + "_NG_crime.csv"
  df = pd.read_csv(filename)
  data.append(df)

df= pd.concat(data)
del data

## Check the Data Frame
df

## Crime EventCodes with Meaning

CODES = {
    84: "Release Person",
    841: "Release Person",
    87: "De-escalate Military Engagement",
    874: "Surrender Millitarily",
    90: "Ivestigate",
    91: "Investigate Crime, Corruption",
    130: "Threaten",
    1383: "Threaten to attack",
    1385: "Threaten Unconventional Mass Violence",
    1711: "Confiscate Property",
    1712: "Destroy Property",
    173: "Arrest",
    176: "Cyber Attack",
    180: "Use Unconventional Violence",
    181: "Abduct, Kidnap or Take Hostage",
    182: "Physically Assault",
    1821: "Sexually Assault",
    1822: "Torture",
    1823: "Kill by Physical Assault",
    183: "Conduct Suicide",
    1831: "Carry Out Suicide Bombing",
    1832: "Carry Out a Vehicular Bombing",
    1833: "Carry Out a Roadside Bombing",
    1834: "Carry Out Location Bombing",
    185: "Attempt to Assasinate",
    186: "Assasinate",
    190: "Murder by Use of Unconventional Military Force",
    191: "Impose Blockade or Restrict Movement",
    193: "Fight with Small Arms and Light Weapons",
    194: " Fight with Artillery and Tanks",
    195: "Employ Aerial Weapons",
    202: "Engage in Mass Killing",
    202: "Engage in Ethnic Cleansing",
    204: "Use Weapons of Mass Destruction",
}

## how to stored event codes to the map

df["EventName"] = df["EventCode"].map(CODES) 
df["EventName"]

## to grup the event date

df_date = df.groupby("Date")["GlobalEventID"].count()
## to plt
df_date.plot()

## Check the Data Frame

df_date

## import plotly

import plotly.express as px

## Code to Plot the Map

fig = px.scatter_mapbox(
    df, 
    lat="ActionGeo_Lat", 
    lon="ActionGeo_Long", 
    color="EventCode",
    hover_name="EventName", 
    # hover_data=["CODES", "SOURCEURL"],
    # size="NumMentions",
    center={'lat':12, 'lon':8},
    zoom=3,
    mapbox_style='open-street-map'
)

## to plot the map use

fig



##### SLIDES_FOR_PROJECT_PRESENTATION
[ABW Fellowship_Final PP_SlideDeck_Mukhtar Abdulhameed.pptx](https://github.com/Analytics-for-a-Better-World/ABW-Academy/files/10165689/ABW.Fellowship_Final.PP_SlideDeck_Mukhtar.Abdulhameed.pptx)


###CODES_USED_FOR_THE_PROJECT

https://colab.research.google.com/drive/1PLEvDGmsvMfq98_gHhlnIEMHOzYYiVw_#scrollTo=dg6rnGacsJ6W

https://colab.research.google.com/drive/1IT61w4U1DeKLZKSW97geSOPcGL6gvvCS#scrollTo=zYfDRRHH226M

