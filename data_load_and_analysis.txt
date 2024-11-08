/* The SQL below was written using sample data from CMS. This was originally written for a MySQL database with INFILE load settings enabled and may need to be adjusted for use in other database systems.
 The data can be found at: https://www.cms.gov/data-research/statistics-trends-and-reports/medicare-claims-synthetic-public-use-files/cms-2008-2010-data-entrepreneurs-synthetic-public-use-file-de-synpuf/de10-sample-1
 /*

-- Re-creating database
DROP DATABASE IF EXISTS desynpuf_data_2008;
CREATE DATABASE desynpuf_data_2008;
USE desynpuf_data_2008;

-- Ensuring table does not exist in new database
DROP TABLE IF EXISTS source_data_beneficiary_summary;

-- Creating empty table to load beneficiary data
CREATE TABLE source_data_beneficiary_summary (
	DESYNPUF_ID varchar(16) DEFAULT NULL,
    ENE_BIRTH_DT varchar(8) DEFAULT NULL,
    ENE_DEATH_DT varchar(8) DEFAULT NULL,
    ENE_SEX_IDENT_CD varchar(1) DEFAULT NULL,
    ENE_RACE_CD varchar(1) DEFAULT NULL,
    ENE_ESRD_IND varchar(1) DEFAULT NULL,
    P_STATE_CODE varchar(2) DEFAULT NULL,
    ENE_COUNTY_CD varchar(3) DEFAULT NULL,
    ENE_HI_CVRAGE_TOT_MONS varchar(2) DEFAULT NULL,
    ENE_SMI_CVRAGE_TOT_MONS varchar(2) DEFAULT NULL,
    ENE_HMO_CVRAGE_TOT_MONS varchar(2) DEFAULT NULL,
    LAN_CVRG_MOS_NUM varchar(1) DEFAULT NULL,
    P_ALZHDMTA varchar(1) DEFAULT NULL,
    P_CHF varchar(1) DEFAULT NULL,
    P_CHRNKIDN varchar(1) DEFAULT NULL,
    P_CNCR varchar(1) DEFAULT NULL,
    P_COPD varchar(1) DEFAULT NULL,
    P_DEPRESSN varchar(1) DEFAULT NULL,
    P_DIABETES varchar(1) DEFAULT NULL,
    P_ISCHMCHT varchar(1) DEFAULT NULL,
    P_OSTEOPRS varchar(1) DEFAULT NULL,
    P_RA_OA varchar(1) DEFAULT NULL,
    P_STRKETIA varchar(1) DEFAULT NULL,
    EDREIMB_IP decimal(12,2) DEFAULT NULL,
    ENRES_IP decimal(12,2) DEFAULT NULL,
    PPYMT_IP decimal(12,2) DEFAULT NULL,
    EDREIMB_OP decimal(12,2) DEFAULT NULL,
    ENRES_OP decimal(12,2) DEFAULT NULL,
    PPYMT_OP decimal(12,2) DEFAULT NULL,
    EDREIMB_CAR decimal(12,2) DEFAULT NULL,
    ENRES_CAR decimal(12,2) DEFAULT NULL,
    PPYMT_CAR decimal(12,2) DEFAULT NULL 
);

-- Loading data from local CSV file
LOAD DATA LOCAL INFILE 'FILEPATH/DE1_0_2008_Beneficiary_Summary_File_Sample_1.csv'
INTO TABLE source_data_beneficiary_summary 
FIELDS TERMINATED BY ','
LINES  TERMINATED BY '\r\n'
IGNORE 1 LINES
(
    DESYNPUF_ID,
    BENE_BIRTH_DT,
    BENE_DEATH_DT,
    BENE_SEX_IDENT_CD,
    BENE_RACE_CD,
    BENE_ESRD_IND,
    SP_STATE_CODE,
    BENE_COUNTY_CD,
    BENE_HI_CVRAGE_TOT_MONS,
    BENE_SMI_CVRAGE_TOT_MONS,
    BENE_HMO_CVRAGE_TOT_MONS,
    PLAN_CVRG_MOS_NUM,
    SP_ALZHDMTA,
    SP_CHF,
    SP_CHRNKIDN,
    SP_CNCR,
    SP_COPD,
    SP_DEPRESSN,
    SP_DIABETES,
    SP_ISCHMCHT,
    SP_OSTEOPRS,
    SP_RA_OA,
    SP_STRKETIA,
    MEDREIMB_IP,
    BENRES_IP,
    PPPYMT_IP,
    MEDREIMB_OP,
    BENRES_OP,
    PPPYMT_OP,
    MEDREIMB_CAR,
    BENRES_CAR,
    PPPYMT_CAR ); 

-- Adding index
ALTER TABLE source_data_beneficiary_summary ADD INDEX (DESYNPUF_ID);

-- Ensuring table does not exist in new database
DROP TABLE IF EXISTS source_data_outpatient_claims;

-- Creating empty table to load outpatient claims data
CREATE TABLE source_data_outpatient_claims (
    DESYNPUF_ID varchar(16) DEFAULT NULL,
    CLM_ID varchar(15) DEFAULT NULL,
    SEGMENT varchar(1) DEFAULT NULL,
    CLM_FROM_DT varchar(8) DEFAULT NULL,
    CLM_THRU_DT varchar(8) DEFAULT NULL,
    PRVDR_NUM varchar(6) DEFAULT NULL,
    CLM_PMT_AMT decimal(12,2) DEFAULT NULL,
    NCH_PRMRY_PYR_CLM_PD_AMT decimal(12,2) DEFAULT NULL,
    AT_PHYSN_NPI varchar(10) DEFAULT NULL,
    OP_PHYSN_NPI varchar(10) DEFAULT NULL,
    OT_PHYSN_NPI varchar(10) DEFAULT NULL,
    NCH_BENE_BLOOD_DDCTBL_LBLTY_AM (12,2) DEFAULT NULL,
	ICD9_DGNS_CD_1 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_2 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_3 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_4 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_5 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_6 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_7 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_8 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_9 varchar(10) DEFAULT NULL,
	ICD9_DGNS_CD_10 varchar(10) DEFAULT NULL,
	ICD9_PRCDR_CD_1 varchar(10) DEFAULT NULL,
	ICD9_PRCDR_CD_2 varchar(10) DEFAULT NULL,
	ICD9_PRCDR_CD_3 varchar(10) DEFAULT NULL,
	ICD9_PRCDR_CD_4 varchar(10) DEFAULT NULL,
	ICD9_PRCDR_CD_5 varchar(10) DEFAULT NULL,
	ICD9_PRCDR_CD_6 varchar(10) DEFAULT NULL,
	NCH_BENE_PTB_DDCTBL_AMT decimal(12,2) DEFAULT NULL,
	NCH_BENE_PTB_COINSRNC_AMT decimal(12,2) DEFAULT NULL,
	ADMTNG_ICD9_DGNS_CD varchar(10) DEFAULT NULL,
	HCPCS_CD_1 varchar(5) DEFAULT NULL,
	HCPCS_CD_2 varchar(5) DEFAULT NULL,
	HCPCS_CD_3 varchar(5) DEFAULT NULL,
	HCPCS_CD_4 varchar(5) DEFAULT NULL,
	HCPCS_CD_5 varchar(5) DEFAULT NULL,
	HCPCS_CD_6 varchar(5) DEFAULT NULL,
	HCPCS_CD_7 varchar(5) DEFAULT NULL,
	HCPCS_CD_8 varchar(5) DEFAULT NULL,
	HCPCS_CD_9 varchar(5) DEFAULT NULL,
	HCPCS_CD_10 varchar(5) DEFAULT NULL,
	HCPCS_CD_11 varchar(5) DEFAULT NULL,
	HCPCS_CD_12 varchar(5) DEFAULT NULL,
	HCPCS_CD_13 varchar(5) DEFAULT NULL,
	HCPCS_CD_14 varchar(5) DEFAULT NULL,
	HCPCS_CD_15 varchar(5) DEFAULT NULL,
	HCPCS_CD_16 varchar(5) DEFAULT NULL,
	HCPCS_CD_17 varchar(5) DEFAULT NULL,
	HCPCS_CD_18 varchar(5) DEFAULT NULL,
	HCPCS_CD_19 varchar(5) DEFAULT NULL,
	HCPCS_CD_20 varchar(5) DEFAULT NULL,
	HCPCS_CD_21 varchar(5) DEFAULT NULL,
	HCPCS_CD_22 varchar(5) DEFAULT NULL,
	HCPCS_CD_23 varchar(5) DEFAULT NULL,
	HCPCS_CD_24 varchar(5) DEFAULT NULL,
	HCPCS_CD_25 varchar(5) DEFAULT NULL,
	HCPCS_CD_26 varchar(5) DEFAULT NULL,
	HCPCS_CD_27 varchar(5) DEFAULT NULL,
	HCPCS_CD_28 varchar(5) DEFAULT NULL,
	HCPCS_CD_29 varchar(5) DEFAULT NULL,
	HCPCS_CD_30 varchar(5) DEFAULT NULL,
	HCPCS_CD_31 varchar(5) DEFAULT NULL,
	HCPCS_CD_32 varchar(5) DEFAULT NULL,
	HCPCS_CD_33 varchar(5) DEFAULT NULL,
	HCPCS_CD_34 varchar(5) DEFAULT NULL,
	HCPCS_CD_35 varchar(5) DEFAULT NULL,
	HCPCS_CD_36 varchar(5) DEFAULT NULL,
	HCPCS_CD_37 varchar(5) DEFAULT NULL,
	HCPCS_CD_38 varchar(5) DEFAULT NULL,
	HCPCS_CD_39 varchar(5) DEFAULT NULL,
	HCPCS_CD_40 varchar(5) DEFAULT NULL,
	HCPCS_CD_41 varchar(5) DEFAULT NULL,
	HCPCS_CD_42 varchar(5) DEFAULT NULL,
	HCPCS_CD_43 varchar(5) DEFAULT NULL,
	HCPCS_CD_44 varchar(5) DEFAULT NULL,
	HCPCS_CD_45 varchar(5) DEFAULT NULL
);

-- Loading data from local CSV file
LOAD DATA LOCAL INFILE 'C:/FILEPATH/DE1_0_2008_to_2010_Outpatient_Claims_Sample_1.csv'
INTO TABLE source_data_outpatient_claims 
FIELDS TERMINATED BY ','
LINES  TERMINATED BY '\r\n'
IGNORE 1 LINES
(
    DESYNPUF_ID,
    CLM_ID,
    SEGMENT,
    CLM_FROM_DT,
    CLM_THRU_DT,
    PRVDR_NUM,
    CLM_PMT_AMT,
    NCH_PRMRY_PYR_CLM_PD_AMT,
    AT_PHYSN_NPI,
    OP_PHYSN_NPI,
    OT_PHYSN_NPI,
    NCH_BENE_BLOOD_DDCTBL_LBLTY_AM,
    ICD9_DGNS_CD_1,
    ICD9_DGNS_CD_2,
    ICD9_DGNS_CD_3,
    ICD9_DGNS_CD_4,
    ICD9_DGNS_CD_5,
    ICD9_DGNS_CD_6,
    ICD9_DGNS_CD_7,
    ICD9_DGNS_CD_8,
    ICD9_DGNS_CD_9,
    ICD9_DGNS_CD_10,
    ICD9_PRCDR_CD_1,
    ICD9_PRCDR_CD_2,
    ICD9_PRCDR_CD_3,
    ICD9_PRCDR_CD_4,
    ICD9_PRCDR_CD_5,
    ICD9_PRCDR_CD_6,
    NCH_BENE_PTB_DDCTBL_AMT,
    NCH_BENE_PTB_COINSRNC_AMT,
    ADMTNG_ICD9_DGNS_CD,
    HCPCS_CD_1,
    HCPCS_CD_2,
    HCPCS_CD_3,
    HCPCS_CD_4,
    HCPCS_CD_5,
    HCPCS_CD_6,
    HCPCS_CD_7,
    HCPCS_CD_8,
    HCPCS_CD_9,
    HCPCS_CD_10,
    HCPCS_CD_11,
    HCPCS_CD_12,
    HCPCS_CD_13,
    HCPCS_CD_14,
    HCPCS_CD_15,
    HCPCS_CD_16,
    HCPCS_CD_17,
    HCPCS_CD_18,
    HCPCS_CD_19,
    HCPCS_CD_20,
    HCPCS_CD_21,
    HCPCS_CD_22,
    HCPCS_CD_23,
    HCPCS_CD_24,
    HCPCS_CD_25,
    HCPCS_CD_26,
    HCPCS_CD_27,
    HCPCS_CD_28,
    HCPCS_CD_29,
    HCPCS_CD_30,
    HCPCS_CD_31,
    HCPCS_CD_32,
    HCPCS_CD_33,
    HCPCS_CD_34,
    HCPCS_CD_35,
    HCPCS_CD_36,
    HCPCS_CD_37,
    HCPCS_CD_38,
    HCPCS_CD_39,
    HCPCS_CD_40,
    HCPCS_CD_41,
    HCPCS_CD_42,
    HCPCS_CD_43,
    HCPCS_CD_44,
    HCPCS_CD_45 ); 

-- Adding index
ALTER TABLE source_data_outpatient_claims ADD INDEX (DESYNPUF_ID);

-- Adding beneficiary data to claims and removing unneeded data
CREATE TABLE claims_beneficiary AS
SELECT distinct
    a.DESYNPUF_ID as beneficiary_id, 
    date_parse(BENE_BIRTH_DT,'%Y%m%d') as date_of_birth,
    date_parse(BENE_DEATH_DT,'%Y%m%d') as date_of_death,
    BENE_SEX_IDENT_CD as sex,
    SP_STATE_CODE as state,
    BENE_HI_CVRAGE_TOT_MONS as part_a_months,
    BENE_SMI_CVRAGE_TOT_MONS as part_b_months,
    BENE_HMO_CVRAGE_TOT_MONS as hmo_months,
    PLAN_CVRG_MOS_NUM as part_d_months,
    MEDREIMB_IP as ip_med_reimb,
    BENRES_IP as ip_bene_reimb,
    PPPYMT_IP as ip_pp_reimb,
    MEDREIMB_OP as op_med_reimb,
    BENRES_OP as op_bene_reimb,
    PPPYMT_OP as op_pp_reimb,
    MEDREIMB_CAR as car_pp_reimb,
    BENRES_CAR as car_bene_reimb,
    PPPYMT_CAR as car_med_reimb,
    CLM_ID as claim_id,
    date_parse(CLM_FROM_DT,'%Y%m%d') as claim_start,
    date_parse(CLM_THRU_DT,'%Y%m%d') as claim_end,
    CLM_PMT_AMT as claim_amount, 
    CONCAT(
    IFNULL(CONCAT(ICD9_DGNS_CD_1, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_2, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_3, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_4, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_5, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_6, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_7, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_8, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_9, ', '), ''),
    IFNULL(CONCAT(ICD9_DGNS_CD_10, ', '), ''),
    IFNULL(CONCAT(ADMTNG_ICD9_DGNS_CD, ''), '')
    ) AS dx_codes_combined,
    CONCAT(
    IFNULL(CONCAT(ICD9_PRCDR_CD_1, ', '), ''),
    IFNULL(CONCAT(ICD9_PRCDR_CD_2, ', '), ''),
    IFNULL(CONCAT(ICD9_PRCDR_CD_3, ', '), ''),
    IFNULL(CONCAT(ICD9_PRCDR_CD_4, ', '), ''),
    IFNULL(CONCAT(ICD9_PRCDR_CD_5, ', '), ''),
    IFNULL(CONCAT(ICD9_PRCDR_CD_6, ''), '')
    ) AS procedure_codes_combined
FROM
    source_data_beneficiary_summary a
INNER JOIN
    source_data_outpatient_claims b
WHERE a.DESYNPUF_ID = b.DESYNPUF_ID
AND LEFT(CLM_THRU_DT,4) = '2008'
AND (CAST(LEFT(BENE_DEATH_DT, 4) AS UNSIGNED) > 2008
   OR date_column IS NULL)
;

-- Combining diagnosis codes into one column for easier analysis
CREATE TABLE dx_codes_unnested AS
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_1 as dx_code
WHERE ICD9_DGNS_CD_1 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_2 as dx_code
WHERE ICD9_DGNS_CD_2 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_3 as dx_code
WHERE ICD9_DGNS_CD_3 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_4 as dx_code
WHERE ICD9_DGNS_CD_4 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_5 as dx_code
WHERE ICD9_DGNS_CD_5 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_6 as dx_code
WHERE ICD9_DGNS_CD_6 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_7 as dx_code
WHERE ICD9_DGNS_CD_7 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_8 as dx_code
WHERE ICD9_DGNS_CD_8 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_9 as dx_code
WHERE ICD9_DGNS_CD_9 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
UNION
SELECT 
    DESYNPUF_ID as beneficiary_id,
    ICD9_DGNS_CD_10 as dx_code
WHERE ICD9_DGNS_CD_10 IS NOT NULL
AND LEFT(CLM_THRU_DT,4) = '2008'
;

-- Basic statistics for analysis

-- Count and frequency of dx codes
SELECT 
dx_code,
COUNT(*) AS count,
(COUNT(*) / (SELECT COUNT(*) FROM dx_codes_unnested)) * 100 AS frequency
FROM dx_codes_unnested
GROUP BY dx_code
ORDER BY frequency DESC;

-- Average number of codes per person
SELECT AVG(total_codes) AS avg_codes_per_beneficiary
FROM (
    SELECT beneficiary_id, COUNT(*) AS total_codes
    FROM dx_codes_unnested
    GROUP BY beneficiary_id
) AS subquery;

-- Frequency of two codes together
SELECT COUNT(DISTINCT a.beneficiary_id) AS two_code_count,
(COUNT(DISTINCT a.beneficiary_id) / (SELECT COUNT(*) FROM dx_codes_unnested)) * 100 AS percentage
FROM dx_codes_unnested AS a
JOIN dx_codes_unnested AS b ON a.beneficiary_id = b.beneficiary_id 
/* Select different codes as needed for analysis */
AND a.dx_code = 'V5832'
AND b.dx_code = 'V5861';