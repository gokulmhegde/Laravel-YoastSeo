<template>
    <div class="container">
        <div class="row">
            <div class="col-md-12 py-3 ">
               <form @submit.prevent="yoastFormSubmit" id="formSubmit">
                  <div class="alert alert-info" role="alert">
                    <h3>Yoast form</h3>
                    <hr>
                    <dl class="row">
                      <dt class="col-sm-3">[text]</dt>
                      <dd class="col-sm-9">The text to use in the analysis.</dd>
                      <dt class="col-sm-3">[attributes.keyword]</dt>
                      <dd class="col-sm-9">The main keyword.</dd>
                      <dt class="col-sm-3">[attributes.synonyms]</dt>
                      <dd class="col-sm-9">The main keyword's synonyms.</dd>
                      <dt class="col-sm-3">[attributes.title]</dt>
                      <dd class="col-sm-9">The SEO title.</dd>
                      <dt class="col-sm-3">[attributes.description]</dt>
                      <dd class="col-sm-9">The SEO description.</dd>
                      <dt class="col-sm-3">[attributes.titleWidth]</dt>
                      <dd class="col-sm-9">The width of the title in pixels.</dd>
                      <dt class="col-sm-3">[attributes.url]</dt>
                      <dd class="col-sm-9">The slug.</dd>
                      <dt class="col-sm-3">[attributes.permalink]</dt>
                      <dd class="col-sm-9">The base url + slug.</dd>
                      <dt class="col-sm-3">[attributes.locale]</dt>
                      <dd class="col-sm-9">The locale.</dd>
                    </dl>
                  </div>
                  <hr>

                  <div class="form-group">
                    <label for="exampleFormControlTextarea1">Text</label>
                    <textarea class="form-control" :class="{'input': true, 'is-danger': errors.has('text') }" v-validate="'required'" id="exampleFormControlTextarea1" rows="3" v-model="text" name="text" placeholder="text"></textarea>
                    <i v-show="errors.has('text')" class="fa fa-warning"></i>
                    <span v-show="errors.has('text')" class="help is-danger">{{ errors.first('text') }}</span>
                  </div>

                  <div class="form-group">
                    <label for="exampleFormControlInput1">Keyword</label>
                    <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="keyword" v-model="keyword" name="keyword" :class="{'input': true, 'is-danger': errors.has('keyword') }" v-validate="'required'">
                    <i v-show="errors.has('keyword')" class="fa fa-warning"></i>
                    <span v-show="errors.has('keyword')" class="help is-danger">{{ errors.first('keyword') }}</span>
                  </div>

                  <div class="form-group">
                    <label for="exampleFormControlInput1">Synonyms</label>
                    <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="synonyms" v-model="synonyms" name="synonyms" :class="{'input': true, 'is-danger': errors.has('synonyms') }" v-validate="'required'">
                    <i v-show="errors.has('synonyms')" class="fa fa-warning"></i>
                    <span v-show="errors.has('synonyms')" class="help is-danger">{{ errors.first('synonyms') }}</span>
                  </div>

                  <div class="form-group">
                    <label for="exampleFormControlInput1">Title</label>
                    <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="title" v-model="title" name="title" :class="{'input': true, 'is-danger': errors.has('title') }" v-validate="'required'">
                    <i v-show="errors.has('title')" class="fa fa-warning"></i>
                    <span v-show="errors.has('title')" class="help is-danger">{{ errors.first('title') }}</span>
                  </div>

                  <div class="form-group">
                    <label for="exampleFormControlInput1">Title width</label>
                    <input type="number" class="form-control" :class="{'input': true, 'is-danger': errors.has('titleWidth') }" v-validate="'required'" id="exampleFormControlInput1" placeholder="titleWidth" v-model="titleWidth" value="920" name="titleWidth">
                    <i v-show="errors.has('titleWidth')" class="fa fa-warning"></i>
                    <span v-show="errors.has('titleWidth')" class="help is-danger">{{ errors.first('titleWidth') }}</span>
                  </div>
                  
                  <div class="form-group">
                    <label for="exampleFormControlTextarea1">Description</label>
                    <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" v-model="description" placeholder="description" name="description" :class="{'input': true, 'is-danger': errors.has('description') }" v-validate="'required'"></textarea>
                    <i v-show="errors.has('description')" class="fa fa-warning"></i>
                    <span v-show="errors.has('description')" class="help is-danger">{{ errors.first('description') }}</span>
                  </div>

                  <div class="form-group">
                    <label for="exampleFormControlTextarea1">URL</label>
                    <input type="text" class="form-control" :class="{'input': true, 'is-danger': errors.has('url') }" v-validate="'required'" id="exampleFormControlInput1" placeholder="url" v-model="url" name="url">
                    <i v-show="errors.has('url')" class="fa fa-warning"></i>
                    <span v-show="errors.has('url')" class="help is-danger">{{ errors.first('url') }}</span>
                  </div>

                  <div class="form-group">
                    <label for="exampleFormControlTextarea1">Permalink</label>
                    <input type="text" class="form-control" :class="{'input': true, 'is-danger': errors.has('permalink') }" v-validate="'required'" id="exampleFormControlInput1" placeholder="permalink" v-model="permalink" name="permalink">
                    <i v-show="errors.has('permalink')" class="fa fa-warning"></i>
                    <span v-show="errors.has('permalink')" class="help is-danger">{{ errors.first('permalink') }}</span>
                  </div>

                  <div class="form-group">
                    <label for="exampleFormControlSelect1">Select locale</label>
                    <select class="form-control" :class="{'input': true, 'is-danger': errors.has('en_locale') }" v-validate="'required'" id="exampleFormControlSelect1" v-model="en_locale" name="en_locale">
                        <option value='af'>af</option>
                        <option value='af_NA'>af_NA</option>
                        <option value='af_ZA'>af_ZA</option>
                        <option value='ak'>ak</option>
                        <option value='ak_GH'>ak_GH</option>
                        <option value='am'>am</option>
                        <option value='am_ET'>am_ET</option>
                        <option value='ar'>ar</option>
                        <option value='ar_AE'>ar_AE</option>
                        <option value='ar_BH'>ar_BH</option>
                        <option value='ar_DJ'>ar_DJ</option>
                        <option value='ar_DZ'>ar_DZ</option>
                        <option value='ar_EG'>ar_EG</option>
                        <option value='ar_EH'>ar_EH</option>
                        <option value='ar_ER'>ar_ER</option>
                        <option value='ar_IL'>ar_IL</option>
                        <option value='ar_IQ'>ar_IQ</option>
                        <option value='ar_JO'>ar_JO</option>
                        <option value='ar_KM'>ar_KM</option>
                        <option value='ar_KW'>ar_KW</option>
                        <option value='ar_LB'>ar_LB</option>
                        <option value='ar_LY'>ar_LY</option>
                        <option value='ar_MA'>ar_MA</option>
                        <option value='ar_MR'>ar_MR</option>
                        <option value='ar_OM'>ar_OM</option>
                        <option value='ar_PS'>ar_PS</option>
                        <option value='ar_QA'>ar_QA</option>
                        <option value='ar_SA'>ar_SA</option>
                        <option value='ar_SD'>ar_SD</option>
                        <option value='ar_SO'>ar_SO</option>
                        <option value='ar_SS'>ar_SS</option>
                        <option value='ar_SY'>ar_SY</option>
                        <option value='ar_TD'>ar_TD</option>
                        <option value='ar_TN'>ar_TN</option>
                        <option value='ar_YE'>ar_YE</option>
                        <option value='as'>as</option>
                        <option value='as_IN'>as_IN</option>
                        <option value='az'>az</option>
                        <option value='az_AZ'>az_AZ</option>
                        <option value='az_Cyrl'>az_Cyrl</option>
                        <option value='az_Cyrl_AZ'>az_Cyrl_AZ</option>
                        <option value='az_Latn'>az_Latn</option>
                        <option value='az_Latn_AZ'>az_Latn_AZ</option>
                        <option value='be'>be</option>
                        <option value='be_BY'>be_BY</option>
                        <option value='bg'>bg</option>
                        <option value='bg_BG'>bg_BG</option>
                        <option value='bm'>bm</option>
                        <option value='bm_Latn'>bm_Latn</option>
                        <option value='bm_Latn_ML'>bm_Latn_ML</option>
                        <option value='bn'>bn</option>
                        <option value='bn_BD'>bn_BD</option>
                        <option value='bn_IN'>bn_IN</option>
                        <option value='bo'>bo</option>
                        <option value='bo_CN'>bo_CN</option>
                        <option value='bo_IN'>bo_IN</option>
                        <option value='br'>br</option>
                        <option value='br_FR'>br_FR</option>
                        <option value='bs'>bs</option>
                        <option value='bs_BA'>bs_BA</option>
                        <option value='bs_Cyrl'>bs_Cyrl</option>
                        <option value='bs_Cyrl_BA'>bs_Cyrl_BA</option>
                        <option value='bs_Latn'>bs_Latn</option>
                        <option value='bs_Latn_BA'>bs_Latn_BA</option>
                        <option value='ca'>ca</option>
                        <option value='ca_AD'>ca_AD</option>
                        <option value='ca_ES'>ca_ES</option>
                        <option value='ca_FR'>ca_FR</option>
                        <option value='ca_IT'>ca_IT</option>
                        <option value='cs'>cs</option>
                        <option value='cs_CZ'>cs_CZ</option>
                        <option value='cy'>cy</option>
                        <option value='cy_GB'>cy_GB</option>
                        <option value='da'>da</option>
                        <option value='da_DK'>da_DK</option>
                        <option value='da_GL'>da_GL</option>
                        <option value='de'>de</option>
                        <option value='de_AT'>de_AT</option>
                        <option value='de_BE'>de_BE</option>
                        <option value='de_CH'>de_CH</option>
                        <option value='de_DE'>de_DE</option>
                        <option value='de_LI'>de_LI</option>
                        <option value='de_LU'>de_LU</option>
                        <option value='dz'>dz</option>
                        <option value='dz_BT'>dz_BT</option>
                        <option value='ee'>ee</option>
                        <option value='ee_GH'>ee_GH</option>
                        <option value='ee_TG'>ee_TG</option>
                        <option value='el'>el</option>
                        <option value='el_CY'>el_CY</option>
                        <option value='el_GR'>el_GR</option>
                        <option value='en'>en</option>
                        <option value='en_AG'>en_AG</option>
                        <option value='en_AI'>en_AI</option>
                        <option value='en_AS'>en_AS</option>
                        <option value='en_AU'>en_AU</option>
                        <option value='en_BB'>en_BB</option>
                        <option value='en_BE'>en_BE</option>
                        <option value='en_BM'>en_BM</option>
                        <option value='en_BS'>en_BS</option>
                        <option value='en_BW'>en_BW</option>
                        <option value='en_BZ'>en_BZ</option>
                        <option value='en_CA'>en_CA</option>
                        <option value='en_CC'>en_CC</option>
                        <option value='en_CK'>en_CK</option>
                        <option value='en_CM'>en_CM</option>
                        <option value='en_CX'>en_CX</option>
                        <option value='en_DG'>en_DG</option>
                        <option value='en_DM'>en_DM</option>
                        <option value='en_ER'>en_ER</option>
                        <option value='en_FJ'>en_FJ</option>
                        <option value='en_FK'>en_FK</option>
                        <option value='en_FM'>en_FM</option>
                        <option value='en_GB'>en_GB</option>
                        <option value='en_GD'>en_GD</option>
                        <option value='en_GG'>en_GG</option>
                        <option value='en_GH'>en_GH</option>
                        <option value='en_GI'>en_GI</option>
                        <option value='en_GM'>en_GM</option>
                        <option value='en_GU'>en_GU</option>
                        <option value='en_GY'>en_GY</option>
                        <option value='en_HK'>en_HK</option>
                        <option value='en_IE'>en_IE</option>
                        <option value='en_IM'>en_IM</option>
                        <option value='en_IN'>en_IN</option>
                        <option value='en_IO'>en_IO</option>
                        <option value='en_JE'>en_JE</option>
                        <option value='en_JM'>en_JM</option>
                        <option value='en_KE'>en_KE</option>
                        <option value='en_KI'>en_KI</option>
                        <option value='en_KN'>en_KN</option>
                        <option value='en_KY'>en_KY</option>
                        <option value='en_LC'>en_LC</option>
                        <option value='en_LR'>en_LR</option>
                        <option value='en_LS'>en_LS</option>
                        <option value='en_MG'>en_MG</option>
                        <option value='en_MH'>en_MH</option>
                        <option value='en_MO'>en_MO</option>
                        <option value='en_MP'>en_MP</option>
                        <option value='en_MS'>en_MS</option>
                        <option value='en_MT'>en_MT</option>
                        <option value='en_MU'>en_MU</option>
                        <option value='en_MW'>en_MW</option>
                        <option value='en_MY'>en_MY</option>
                        <option value='en_NA'>en_NA</option>
                        <option value='en_NF'>en_NF</option>
                        <option value='en_NG'>en_NG</option>
                        <option value='en_NR'>en_NR</option>
                        <option value='en_NU'>en_NU</option>
                        <option value='en_NZ'>en_NZ</option>
                        <option value='en_PG'>en_PG</option>
                        <option value='en_PH'>en_PH</option>
                        <option value='en_PK'>en_PK</option>
                        <option value='en_PN'>en_PN</option>
                        <option value='en_PR'>en_PR</option>
                        <option value='en_PW'>en_PW</option>
                        <option value='en_RW'>en_RW</option>
                        <option value='en_SB'>en_SB</option>
                        <option value='en_SC'>en_SC</option>
                        <option value='en_SD'>en_SD</option>
                        <option value='en_SG'>en_SG</option>
                        <option value='en_SH'>en_SH</option>
                        <option value='en_SL'>en_SL</option>
                        <option value='en_SS'>en_SS</option>
                        <option value='en_SX'>en_SX</option>
                        <option value='en_SZ'>en_SZ</option>
                        <option value='en_TC'>en_TC</option>
                        <option value='en_TK'>en_TK</option>
                        <option value='en_TO'>en_TO</option>
                        <option value='en_TT'>en_TT</option>
                        <option value='en_TV'>en_TV</option>
                        <option value='en_TZ'>en_TZ</option>
                        <option value='en_UG'>en_UG</option>
                        <option value='en_UM'>en_UM</option>
                        <option value='en_US'>en_US</option>
                        <option value='en_VC'>en_VC</option>
                        <option value='en_VG'>en_VG</option>
                        <option value='en_VI'>en_VI</option>
                        <option value='en_VU'>en_VU</option>
                        <option value='en_WS'>en_WS</option>
                        <option value='en_ZA'>en_ZA</option>
                        <option value='en_ZM'>en_ZM</option>
                        <option value='en_ZW'>en_ZW</option>
                        <option value='eo'>eo</option>
                        <option value='es'>es</option>
                        <option value='es_AR'>es_AR</option>
                        <option value='es_BO'>es_BO</option>
                        <option value='es_CL'>es_CL</option>
                        <option value='es_CO'>es_CO</option>
                        <option value='es_CR'>es_CR</option>
                        <option value='es_CU'>es_CU</option>
                        <option value='es_DO'>es_DO</option>
                        <option value='es_EA'>es_EA</option>
                        <option value='es_EC'>es_EC</option>
                        <option value='es_ES'>es_ES</option>
                        <option value='es_GQ'>es_GQ</option>
                        <option value='es_GT'>es_GT</option>
                        <option value='es_HN'>es_HN</option>
                        <option value='es_IC'>es_IC</option>
                        <option value='es_MX'>es_MX</option>
                        <option value='es_NI'>es_NI</option>
                        <option value='es_PA'>es_PA</option>
                        <option value='es_PE'>es_PE</option>
                        <option value='es_PH'>es_PH</option>
                        <option value='es_PR'>es_PR</option>
                        <option value='es_PY'>es_PY</option>
                        <option value='es_SV'>es_SV</option>
                        <option value='es_US'>es_US</option>
                        <option value='es_UY'>es_UY</option>
                        <option value='es_VE'>es_VE</option>
                        <option value='et'>et</option>
                        <option value='et_EE'>et_EE</option>
                        <option value='eu'>eu</option>
                        <option value='eu_ES'>eu_ES</option>
                        <option value='fa'>fa</option>
                        <option value='fa_AF'>fa_AF</option>
                        <option value='fa_IR'>fa_IR</option>
                        <option value='ff'>ff</option>
                        <option value='ff_CM'>ff_CM</option>
                        <option value='ff_GN'>ff_GN</option>
                        <option value='ff_MR'>ff_MR</option>
                        <option value='ff_SN'>ff_SN</option>
                        <option value='fi'>fi</option>
                        <option value='fi_FI'>fi_FI</option>
                        <option value='fo'>fo</option>
                        <option value='fo_FO'>fo_FO</option>
                        <option value='fr'>fr</option>
                        <option value='fr_BE'>fr_BE</option>
                        <option value='fr_BF'>fr_BF</option>
                        <option value='fr_BI'>fr_BI</option>
                        <option value='fr_BJ'>fr_BJ</option>
                        <option value='fr_BL'>fr_BL</option>
                        <option value='fr_CA'>fr_CA</option>
                        <option value='fr_CD'>fr_CD</option>
                        <option value='fr_CF'>fr_CF</option>
                        <option value='fr_CG'>fr_CG</option>
                        <option value='fr_CH'>fr_CH</option>
                        <option value='fr_CI'>fr_CI</option>
                        <option value='fr_CM'>fr_CM</option>
                        <option value='fr_DJ'>fr_DJ</option>
                        <option value='fr_DZ'>fr_DZ</option>
                        <option value='fr_FR'>fr_FR</option>
                        <option value='fr_GA'>fr_GA</option>
                        <option value='fr_GF'>fr_GF</option>
                        <option value='fr_GN'>fr_GN</option>
                        <option value='fr_GP'>fr_GP</option>
                        <option value='fr_GQ'>fr_GQ</option>
                        <option value='fr_HT'>fr_HT</option>
                        <option value='fr_KM'>fr_KM</option>
                        <option value='fr_LU'>fr_LU</option>
                        <option value='fr_MA'>fr_MA</option>
                        <option value='fr_MC'>fr_MC</option>
                        <option value='fr_MF'>fr_MF</option>
                        <option value='fr_MG'>fr_MG</option>
                        <option value='fr_ML'>fr_ML</option>
                        <option value='fr_MQ'>fr_MQ</option>
                        <option value='fr_MR'>fr_MR</option>
                        <option value='fr_MU'>fr_MU</option>
                        <option value='fr_NC'>fr_NC</option>
                        <option value='fr_NE'>fr_NE</option>
                        <option value='fr_PF'>fr_PF</option>
                        <option value='fr_PM'>fr_PM</option>
                        <option value='fr_RE'>fr_RE</option>
                        <option value='fr_RW'>fr_RW</option>
                        <option value='fr_SC'>fr_SC</option>
                        <option value='fr_SN'>fr_SN</option>
                        <option value='fr_SY'>fr_SY</option>
                        <option value='fr_TD'>fr_TD</option>
                        <option value='fr_TG'>fr_TG</option>
                        <option value='fr_TN'>fr_TN</option>
                        <option value='fr_VU'>fr_VU</option>
                        <option value='fr_WF'>fr_WF</option>
                        <option value='fr_YT'>fr_YT</option>
                        <option value='fy'>fy</option>
                        <option value='fy_NL'>fy_NL</option>
                        <option value='ga'>ga</option>
                        <option value='ga_IE'>ga_IE</option>
                        <option value='gd'>gd</option>
                        <option value='gd_GB'>gd_GB</option>
                        <option value='gl'>gl</option>
                        <option value='gl_ES'>gl_ES</option>
                        <option value='gu'>gu</option>
                        <option value='gu_IN'>gu_IN</option>
                        <option value='gv'>gv</option>
                        <option value='gv_IM'>gv_IM</option>
                        <option value='ha'>ha</option>
                        <option value='ha_GH'>ha_GH</option>
                        <option value='ha_Latn'>ha_Latn</option>
                        <option value='ha_Latn_GH'>ha_Latn_GH</option>
                        <option value='ha_Latn_NE'>ha_Latn_NE</option>
                        <option value='ha_Latn_NG'>ha_Latn_NG</option>
                        <option value='ha_NE'>ha_NE</option>
                        <option value='ha_NG'>ha_NG</option>
                        <option value='he'>he</option>
                        <option value='he_IL'>he_IL</option>
                        <option value='hi'>hi</option>
                        <option value='hi_IN'>hi_IN</option>
                        <option value='hr'>hr</option>
                        <option value='hr_BA'>hr_BA</option>
                        <option value='hr_HR'>hr_HR</option>
                        <option value='hu'>hu</option>
                        <option value='hu_HU'>hu_HU</option>
                        <option value='hy'>hy</option>
                        <option value='hy_AM'>hy_AM</option>
                        <option value='id'>id</option>
                        <option value='id_ID'>id_ID</option>
                        <option value='ig'>ig</option>
                        <option value='ig_NG'>ig_NG</option>
                        <option value='ii'>ii</option>
                        <option value='ii_CN'>ii_CN</option>
                        <option value='is'>is</option>
                        <option value='is_IS'>is_IS</option>
                        <option value='it'>it</option>
                        <option value='it_CH'>it_CH</option>
                        <option value='it_IT'>it_IT</option>
                        <option value='it_SM'>it_SM</option>
                        <option value='ja'>ja</option>
                        <option value='ja_JP'>ja_JP</option>
                        <option value='ka'>ka</option>
                        <option value='ka_GE'>ka_GE</option>
                        <option value='ki'>ki</option>
                        <option value='ki_KE'>ki_KE</option>
                        <option value='kk'>kk</option>
                        <option value='kk_Cyrl'>kk_Cyrl</option>
                        <option value='kk_Cyrl_KZ'>kk_Cyrl_KZ</option>
                        <option value='kk_KZ'>kk_KZ</option>
                        <option value='kl'>kl</option>
                        <option value='kl_GL'>kl_GL</option>
                        <option value='km'>km</option>
                        <option value='km_KH'>km_KH</option>
                        <option value='kn'>kn</option>
                        <option value='kn_IN'>kn_IN</option>
                        <option value='ko'>ko</option>
                        <option value='ko_KP'>ko_KP</option>
                        <option value='ko_KR'>ko_KR</option>
                        <option value='ks'>ks</option>
                        <option value='ks_Arab'>ks_Arab</option>
                        <option value='ks_Arab_IN'>ks_Arab_IN</option>
                        <option value='ks_IN'>ks_IN</option>
                        <option value='kw'>kw</option>
                        <option value='kw_GB'>kw_GB</option>
                        <option value='ky'>ky</option>
                        <option value='ky_Cyrl'>ky_Cyrl</option>
                        <option value='ky_Cyrl_KG'>ky_Cyrl_KG</option>
                        <option value='ky_KG'>ky_KG</option>
                        <option value='lb'>lb</option>
                        <option value='lb_LU'>lb_LU</option>
                        <option value='lg'>lg</option>
                        <option value='lg_UG'>lg_UG</option>
                        <option value='ln'>ln</option>
                        <option value='ln_AO'>ln_AO</option>
                        <option value='ln_CD'>ln_CD</option>
                        <option value='ln_CF'>ln_CF</option>
                        <option value='ln_CG'>ln_CG</option>
                        <option value='lo'>lo</option>
                        <option value='lo_LA'>lo_LA</option>
                        <option value='lt'>lt</option>
                        <option value='lt_LT'>lt_LT</option>
                        <option value='lu'>lu</option>
                        <option value='lu_CD'>lu_CD</option>
                        <option value='lv'>lv</option>
                        <option value='lv_LV'>lv_LV</option>
                        <option value='mg'>mg</option>
                        <option value='mg_MG'>mg_MG</option>
                        <option value='mk'>mk</option>
                        <option value='mk_MK'>mk_MK</option>
                        <option value='ml'>ml</option>
                        <option value='ml_IN'>ml_IN</option>
                        <option value='mn'>mn</option>
                        <option value='mn_Cyrl'>mn_Cyrl</option>
                        <option value='mn_Cyrl_MN'>mn_Cyrl_MN</option>
                        <option value='mn_MN'>mn_MN</option>
                        <option value='mr'>mr</option>
                        <option value='mr_IN'>mr_IN</option>
                        <option value='ms'>ms</option>
                        <option value='ms_BN'>ms_BN</option>
                        <option value='ms_Latn'>ms_Latn</option>
                        <option value='ms_Latn_BN'>ms_Latn_BN</option>
                        <option value='ms_Latn_MY'>ms_Latn_MY</option>
                        <option value='ms_Latn_SG'>ms_Latn_SG</option>
                        <option value='ms_MY'>ms_MY</option>
                        <option value='ms_SG'>ms_SG</option>
                        <option value='mt'>mt</option>
                        <option value='mt_MT'>mt_MT</option>
                        <option value='my'>my</option>
                        <option value='my_MM'>my_MM</option>
                        <option value='nb'>nb</option>
                        <option value='nb_NO'>nb_NO</option>
                        <option value='nb_SJ'>nb_SJ</option>
                        <option value='nd'>nd</option>
                        <option value='nd_ZW'>nd_ZW</option>
                        <option value='ne'>ne</option>
                        <option value='ne_IN'>ne_IN</option>
                        <option value='ne_NP'>ne_NP</option>
                        <option value='nl'>nl</option>
                        <option value='nl_AW'>nl_AW</option>
                        <option value='nl_BE'>nl_BE</option>
                        <option value='nl_BQ'>nl_BQ</option>
                        <option value='nl_CW'>nl_CW</option>
                        <option value='nl_NL'>nl_NL</option>
                        <option value='nl_SR'>nl_SR</option>
                        <option value='nl_SX'>nl_SX</option>
                        <option value='nn'>nn</option>
                        <option value='nn_NO'>nn_NO</option>
                        <option value='no'>no</option>
                        <option value='no_NO'>no_NO</option>
                        <option value='om'>om</option>
                        <option value='om_ET'>om_ET</option>
                        <option value='om_KE'>om_KE</option>
                        <option value='or'>or</option>
                        <option value='or_IN'>or_IN</option>
                        <option value='os'>os</option>
                        <option value='os_GE'>os_GE</option>
                        <option value='os_RU'>os_RU</option>
                        <option value='pa'>pa</option>
                        <option value='pa_Arab'>pa_Arab</option>
                        <option value='pa_Arab_PK'>pa_Arab_PK</option>
                        <option value='pa_Guru'>pa_Guru</option>
                        <option value='pa_Guru_IN'>pa_Guru_IN</option>
                        <option value='pa_IN'>pa_IN</option>
                        <option value='pa_PK'>pa_PK</option>
                        <option value='pl'>pl</option>
                        <option value='pl_PL'>pl_PL</option>
                        <option value='ps'>ps</option>
                        <option value='ps_AF'>ps_AF</option>
                        <option value='pt'>pt</option>
                        <option value='pt_AO'>pt_AO</option>
                        <option value='pt_BR'>pt_BR</option>
                        <option value='pt_CV'>pt_CV</option>
                        <option value='pt_GW'>pt_GW</option>
                        <option value='pt_MO'>pt_MO</option>
                        <option value='pt_MZ'>pt_MZ</option>
                        <option value='pt_PT'>pt_PT</option>
                        <option value='pt_ST'>pt_ST</option>
                        <option value='pt_TL'>pt_TL</option>
                        <option value='qu'>qu</option>
                        <option value='qu_BO'>qu_BO</option>
                        <option value='qu_EC'>qu_EC</option>
                        <option value='qu_PE'>qu_PE</option>
                        <option value='rm'>rm</option>
                        <option value='rm_CH'>rm_CH</option>
                        <option value='rn'>rn</option>
                        <option value='rn_BI'>rn_BI</option>
                        <option value='ro'>ro</option>
                        <option value='ro_MD'>ro_MD</option>
                        <option value='ro_RO'>ro_RO</option>
                        <option value='ru'>ru</option>
                        <option value='ru_BY'>ru_BY</option>
                        <option value='ru_KG'>ru_KG</option>
                        <option value='ru_KZ'>ru_KZ</option>
                        <option value='ru_MD'>ru_MD</option>
                        <option value='ru_RU'>ru_RU</option>
                        <option value='ru_UA'>ru_UA</option>
                        <option value='rw'>rw</option>
                        <option value='rw_RW'>rw_RW</option>
                        <option value='se'>se</option>
                        <option value='se_FI'>se_FI</option>
                        <option value='se_NO'>se_NO</option>
                        <option value='se_SE'>se_SE</option>
                        <option value='sg'>sg</option>
                        <option value='sg_CF'>sg_CF</option>
                        <option value='sh'>sh</option>
                        <option value='sh_BA'>sh_BA</option>
                        <option value='si'>si</option>
                        <option value='si_LK'>si_LK</option>
                        <option value='sk'>sk</option>
                        <option value='sk_SK'>sk_SK</option>
                        <option value='sl'>sl</option>
                        <option value='sl_SI'>sl_SI</option>
                        <option value='sn'>sn</option>
                        <option value='sn_ZW'>sn_ZW</option>
                        <option value='so'>so</option>
                        <option value='so_DJ'>so_DJ</option>
                        <option value='so_ET'>so_ET</option>
                        <option value='so_KE'>so_KE</option>
                        <option value='so_SO'>so_SO</option>
                        <option value='sq'>sq</option>
                        <option value='sq_AL'>sq_AL</option>
                        <option value='sq_MK'>sq_MK</option>
                        <option value='sq_XK'>sq_XK</option>
                        <option value='sr'>sr</option>
                        <option value='sr_BA'>sr_BA</option>
                        <option value='sr_Cyrl'>sr_Cyrl</option>
                        <option value='sr_Cyrl_BA'>sr_Cyrl_BA</option>
                        <option value='sr_Cyrl_ME'>sr_Cyrl_ME</option>
                        <option value='sr_Cyrl_RS'>sr_Cyrl_RS</option>
                        <option value='sr_Cyrl_XK'>sr_Cyrl_XK</option>
                        <option value='sr_Latn'>sr_Latn</option>
                        <option value='sr_Latn_BA'>sr_Latn_BA</option>
                        <option value='sr_Latn_ME'>sr_Latn_ME</option>
                        <option value='sr_Latn_RS'>sr_Latn_RS</option>
                        <option value='sr_Latn_XK'>sr_Latn_XK</option>
                        <option value='sr_ME'>sr_ME</option>
                        <option value='sr_RS'>sr_RS</option>
                        <option value='sr_XK'>sr_XK</option>
                        <option value='sv'>sv</option>
                        <option value='sv_AX'>sv_AX</option>
                        <option value='sv_FI'>sv_FI</option>
                        <option value='sv_SE'>sv_SE</option>
                        <option value='sw'>sw</option>
                        <option value='sw_CD'>sw_CD</option>
                        <option value='sw_KE'>sw_KE</option>
                        <option value='sw_TZ'>sw_TZ</option>
                        <option value='sw_UG'>sw_UG</option>
                        <option value='ta'>ta</option>
                        <option value='ta_IN'>ta_IN</option>
                        <option value='ta_LK'>ta_LK</option>
                        <option value='ta_MY'>ta_MY</option>
                        <option value='ta_SG'>ta_SG</option>
                        <option value='te'>te</option>
                        <option value='te_IN'>te_IN</option>
                        <option value='th'>th</option>
                        <option value='th_TH'>th_TH</option>
                        <option value='ti'>ti</option>
                        <option value='ti_ER'>ti_ER</option>
                        <option value='ti_ET'>ti_ET</option>
                        <option value='tl'>tl</option>
                        <option value='tl_PH'>tl_PH</option>
                        <option value='to'>to</option>
                        <option value='to_TO'>to_TO</option>
                        <option value='tr'>tr</option>
                        <option value='tr_CY'>tr_CY</option>
                        <option value='tr_TR'>tr_TR</option>
                        <option value='ug'>ug</option>
                        <option value='ug_Arab'>ug_Arab</option>
                        <option value='ug_Arab_CN'>ug_Arab_CN</option>
                        <option value='ug_CN'>ug_CN</option>
                        <option value='uk'>uk</option>
                        <option value='uk_UA'>uk_UA</option>
                        <option value='ur'>ur</option>
                        <option value='ur_IN'>ur_IN</option>
                        <option value='ur_PK'>ur_PK</option>
                        <option value='uz'>uz</option>
                        <option value='uz_AF'>uz_AF</option>
                        <option value='uz_Arab'>uz_Arab</option>
                        <option value='uz_Arab_AF'>uz_Arab_AF</option>
                        <option value='uz_Cyrl'>uz_Cyrl</option>
                        <option value='uz_Cyrl_UZ'>uz_Cyrl_UZ</option>
                        <option value='uz_Latn'>uz_Latn</option>
                        <option value='uz_Latn_UZ'>uz_Latn_UZ</option>
                        <option value='uz_UZ'>uz_UZ</option>
                        <option value='vi'>vi</option>
                        <option value='vi_VN'>vi_VN</option>
                        <option value='yi'>yi</option>
                        <option value='yo'>yo</option>
                        <option value='yo_BJ'>yo_BJ</option>
                        <option value='yo_NG'>yo_NG</option>
                        <option value='zh'>zh</option>
                        <option value='zh_CN'>zh_CN</option>
                        <option value='zh_HK'>zh_HK</option>
                        <option value='zh_Hans'>zh_Hans</option>
                        <option value='zh_Hans_CN'>zh_Hans_CN</option>
                        <option value='zh_Hans_HK'>zh_Hans_HK</option>
                        <option value='zh_Hans_MO'>zh_Hans_MO</option>
                        <option value='zh_Hans_SG'>zh_Hans_SG</option>
                        <option value='zh_Hant'>zh_Hant</option>
                        <option value='zh_Hant_HK'>zh_Hant_HK</option>
                        <option value='zh_Hant_MO'>zh_Hant_MO</option>
                        <option value='zh_Hant_TW'>zh_Hant_TW</option>
                        <option value='zh_MO'>zh_MO</option>
                        <option value='zh_SG'>zh_SG</option>
                        <option value='zh_TW'>zh_TW</option>
                        <option value='zu'>zu</option>
                        <option value='zu_ZA'>zu_ZA</option>
                    </select>
                    <i v-show="errors.has('en_locale')" class="fa fa-warning"></i>
                    <span v-show="errors.has('en_locale')" class="help is-danger">{{ errors.first('en_locale') }}</span>
                  </div>

                  <button type="submit" class="btn btn-primary">Generate data</button>

                </form> 
            </div>
            
            <div v-if="seo.length">
                  <div class="col-md-12">
                    <hr>
                  </div>

                  <div class="mb-3 col-md-12">
                      <h3>SEO assessments</h3>
                      <ul class="bulleted-list">
                        <li class="col-md-12 p-2 pl-0 score seo-score-icon seo-score-text" :class="item.rating" v-for="item in seo" v-html="item.text"></li>
                      </ul>
                  </div>
            </div>

            <div v-if="content.length">
                <div class="col-md-12">
                  <hr>
                </div>
                <div  class="mb-3 col-md-12">
                  <h3>Content assessments</h3>
                  <ul class="bulleted-list">
                    <li class="col-md-12 p-2 pl-0 score seo-score-icon seo-score-text" :class="item.rating" v-for="item in content" v-html="item.text"></li>
                  </ul>
                </div>
            </div>          
            
        </div>
    </div>
</template>

<script>
    import babelPolyfill from 'babel-polyfill';
    import { Paper, ContentAssessor, Researcher, SnippetPreview } from "yoastseo";
    import SEOAssessor from 'yoastseo/src/seoAssessor';
    import zipObject from 'lodash/zipObject'
    import omit from 'lodash/omit'
    import Jed from 'jed';
    import snarkdown from 'snarkdown';
    import Presenter from './Presenter';
    export default {
        data() {
            return {
                text: '',
                keyword: '',
                title: '',
                description: '',
                url: '',
                titleWidth: '',
                en_locale: 'en_US',
                permalink: '',
                synonyms: '',
                seo: [],
                content: []
            }
        },
        methods: {
            yoastFormSubmit(){
                  this.$validator.validateAll().then((result) => {
                    if (result) {
                      const paper = new Paper(this.text, {
                          keyword: this.keyword,
                          title: this.title,
                          description: this.description,
                          url: this.url,
                          metaDescription: this.metaDescription,
                          titleWidth: this.titleWidth,
                          locale: this.en_locale,
                          permalink: this.permalink
                      });

                      const contentAssessor = new ContentAssessor(this.i18n());
                      const seoAssessor = new SEOAssessor(this.i18n());

                      contentAssessor.assess(paper);
                      seoAssessor.assess(paper);

                      const final_scores = this.getScores(seoAssessor, contentAssessor);

                      this.seo = final_scores.seo;
                      this.content = final_scores.content;

                      return;
                    }
                  });     

            },
            getScores(seoAssessor, contentAssessor) {
                return {
                    seo: new Presenter().getScoresWithRatings(seoAssessor),
                    content: new Presenter().getScoresWithRatings(contentAssessor)
                }
            },
            getScoresAsHTML(scores) {
                return new Presenter().getScoresAsHTML(h, scores);
            },
            i18n() {
                return new Jed({
                    domain: `js-text-analysis`,
                    locale_data: {
                        "js-text-analysis": { "": {} }
                    }
                })
            }
        }
    }
</script>
<style scoped>
      hr {
        margin-top: 1rem;
        margin-bottom: 1rem;
        border: 0;
        border-top: 1px solid rgba(0, 0, 0, 0.1);
      }
      .input.is-danger:focus {
          border-color: #dc3545 !important;
          box-shadow: 0 1px 1px rgba(0, 0, 0, 0.075) inset, 0 0 8px #dc3545 !important;
          outline: 0 none;
      }
      .input.is-danger {
          border-color: #dc3545 !important;
      }
      .help.is-danger {
          color: #a94442; 
      }
      ul {
        margin: 0;
        padding: 0;
        list-style: none;
      }
      .bulleted-list .seo-score-icon.bad:before {
        border: 5px solid #dc3232;
      }
      .bulleted-list .seo-score-icon.good:before {
        border: 5px solid #7ad03a;
      }
      .bulleted-list .seo-score-icon.ok:before {
        border: 5px solid #ee7c1b;
      }
      .bulleted-list {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        align-items: flex-start;
      }
      .bulleted-list li:before {
        content: '';
        width: 0;
        height: 0;
        top: 16px;
        left: 0;
        z-index: 1;
        margin-right: 8px;
        position: absolute;
      }
      .bulleted-list li {
        padding-left: 20px!important;
      }
</style>