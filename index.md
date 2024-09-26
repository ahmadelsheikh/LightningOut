<html>
      <head>
            <meta name="viewport" content="width=device-width, initial-scale=1.0" />
            <title>DSP2</title>
            <style>
                .form-container {
                display: flex;
                flex-wrap: wrap;
                }
                .form-group {
                width: 50%;
                padding: 10px;
                box-sizing: border-box;
                }
                .form-group label {
                display: block;
                margin-bottom: 5px;
                }
                .form-group input {
                width: 100%;
                padding: 8px;
                box-sizing: border-box;
                }
                
                .checkbox-container {
                width: 100%;
                padding: 10px;
                box-sizing: border-box;
                }
                .additional-fields {
                display: flex;
                flex-wrap: wrap;
                border-bottom: 1px solid #ccc; /* Separator line */
                margin-bottom: 20px; /* Space below the separator */
                padding-bottom: 20px; /* Padding to make space around the separator */
                }
                .additional-fields .form-group {
                width: 50%;
                }
                
                .hidden {
                display: none;
                }
                
                .spinner {
                display: none; /* Initially hidden */
                border: 8px solid #f3f3f3; /* Light grey */
                border-top: 8px solid #3498db; /* Blue */
                border-radius: 50%;
                width: 60px;
                height: 60px;
                animation: spin 2s linear infinite;
                position: fixed; /* Center the spinner */
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                }
                
                @keyframes spin {
                0% { transform: rotate(0deg); }
                100% { transform: rotate(360deg); }
                }
                
            </style>
        </head>
        <body>

 <div id="inputdata" class="form-container">
                <div class="checkbox-container">
                    <div class="slds-checkbox">
                        <input type="checkbox" name="options" id="toggleCheckbox" />
                        <label class="slds-checkbox__label" for="toggleCheckbox">
                            <span class="slds-checkbox_faux"></span>
                            <span class="slds-form-element__label">Prospect Journey (Y|N)</span>
                        </label>
                    </div>
                </div>
                <div id="additionalFields" class="additional-fields hidden">
                    <div class="form-group">
                        <label for="firstName">First Name:</label>
                        <input type="text" id="firstName" placeholder="First Name…" class="slds-input" />
                    </div>
                    <div class="form-group">
                        <label for="lastName">Last Name:</label>
                        <input type="text" id="lastName" placeholder="Last Name…" class="slds-input" />
                    </div>
                    <div class="form-group">
                        <label for="email">Email:</label>
                        <input type="email" id="email" placeholder="Email…" class="slds-input" />
                    </div>
                    <div class="form-group">
                        <label for="phone">Phone:</label>
                        <input type="tel" id="phone" placeholder="Phone…" class="slds-input" />
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="monthlyPayment">Monthly Payment:</label>
                    <input type="number" id="monthlyPayment" placeholder="Monthly Payment…" class="slds-input" />
                </div>
                <div class="form-group">
                    <label for="basketURL">Basket URL:</label>
                    <input type="text" id="basketURL" placeholder="Basket URL…" class="slds-input" />
                </div>
                <div class="form-group">
                    <label for="mopId">MOPId:</label>
                    <input type="text" id="mopId" placeholder="MOPId…" class="slds-input" />
                </div>
                <div class="form-group">
                    <label for="country">Country:</label>
                    <input type="text" id="country" placeholder="Country…" class="slds-input" />
                </div>
                <div class="form-group">
                    <label for="applicationName">Application Name:</label>
                    <input type="text" id="applicationName" placeholder="Application Name…" class="slds-input" />
                </div>
                
            </div>
            <div id="console">
                <div id="lightningComponent"></div>
            </div>
            <div id="spinner" class="spinner"></div>
<script src="https://omnicanal--f2ml.sandbox.my.salesforce-sites.com/DDDSP2/lightning/lightning.out.js"></script>
    <script>        
    let monthlyPaymentValue = '';
    let basketURLValue = '';
    let mopIdValue = '';
    let countryValue = '';
    let appNameValue = '';
    let firstNameValue = '';
    let lastNameValue = '';
    let emailValue = '';
    let phoneValue = '';
    let typingTimeout;
    let prospectVal=false;
    
    document.addEventListener('DOMContentLoaded', (event) => {
        const monthlyPayment = document.getElementById('monthlyPayment');
        const basketURL = document.getElementById('basketURL');
        const mopId = document.getElementById('mopId');
        const lightningComponent = document.getElementById('lightningComponent');
        
        const prospectCheckbox = document.getElementById('toggleCheckbox');
        const additionalFields = document.getElementById('additionalFields');
        
        /*const toggleCheckbox = document.getElementById('toggleCheckbox');
        const additionalFields = document.getElementById('additionalFields');

            toggleCheckbox.addEventListener('change', () => {
                additionalFields.classList.toggle('hidden', !toggleCheckbox.checked);
            });*/
        
        const country = document.getElementById('country');
        const appName = document.getElementById('applicationName');
        const firstName = document.getElementById('firstName');
        const lastName = document.getElementById('lastName');
        const email = document.getElementById('email');
        const phone = document.getElementById('phone');
        
        function handleInputChange() {
        clearTimeout(typingTimeout);
        
        typingTimeout = setTimeout(() => {
        if (monthlyPaymentValue && basketURLValue && mopIdValue && countryValue && appNameValue) {
        lightningComponent.innerHTML = '';
        const leadData = {
        firstName: firstNameValue,
        lastName: lastNameValue,
        email: emailValue,
        mobile: phoneValue,
        applicationcode: appNameValue,
        country: countryValue,
        installments: monthlyPaymentValue,
        basketurl: basketURLValue,
        mopid: mopIdValue,
        isSellerJourney : !prospectVal,
        isProspectJourney:prospectVal
    }
                              $Lightning.use("c:DSP2ExternalOut", function() {
        $Lightning.createComponent("c:ddDSP2Button", {
            leadData:leadData
        }, "lightningComponent", function(cmp){
            // Some stuff if needed
        });
    },
	"https://omnicanal--f2ml.sandbox.my.salesforce-sites.com/DDDSP2", // Site endpoint
	);
    }
    }, 1000); // 1000 milliseconds = 1 second
    }
    
    monthlyPayment.addEventListener('input', (event) => {
        monthlyPaymentValue = event.target.value;
        console.log('Current monthly payment value:', monthlyPaymentValue);
        handleInputChange();
    });
        
        country.addEventListener('input', (event) => {
        countryValue = event.target.value;
        console.log('Current country value:', countryValue);
        handleInputChange();
    });
        
        appName.addEventListener('input', (event) => {
        appNameValue = event.target.value;
        console.log('Current appName value:', appNameValue);
        handleInputChange();
    });
        
        firstName.addEventListener('input', (event) => {
        firstNameValue = event.target.value;
        console.log('Current first Name value:', firstNameValue);
    });
        
        lastName.addEventListener('input', (event) => {
        lastNameValue = event.target.value;
        console.log('Current last Name value:', lastNameValue);
    });
        
        email.addEventListener('input', (event) => {
        emailValue = event.target.value;
        console.log('Current email value:', emailValue);
    });
        
        phone.addEventListener('input', (event) => {
        phoneValue = event.target.value;
        console.log('Current phone value:', phoneValue);        
    });
        monthlyPayment.addEventListener('input', (event) => {
        monthlyPaymentValue = event.target.value;
        console.log('Current monthly payment value:', monthlyPaymentValue);
        handleInputChange();
    });
        
        basketURL.addEventListener('input', (event) => {
        basketURLValue = event.target.value;
        console.log('Current basket URL value:', basketURLValue);
        handleInputChange();
    });
        
        mopId.addEventListener('input', (event) => {
        mopIdValue = event.target.value;
        console.log('Current MOPId value:', mopIdValue);
        handleInputChange();
    });
        
        
        
        // Event listener for checkbox change
        prospectCheckbox.addEventListener('change', () => {
        additionalFields.classList.toggle('hidden', !prospectCheckbox.checked);
        prospectVal = prospectCheckbox.checked;
    });
    });
        
        //New Code to handle the callback after the journy with OB came to an end
        const queryString = window.location.search;    
        console.log(queryString);
        const urlParams = new URLSearchParams(queryString);
        const connectionId = urlParams.get('connectionId').split(',')[0];
        console.log(connectionId);
        const leadId = urlParams.get('leadid');
        console.log('lead id: ', leadId); 
        const adpId = urlParams.get('adpreq');
        console.log('adpId: ', adpId); 
        if(leadId)
        {
        document.getElementById("spinner").style.display = "block";
        
        $Lightning.use("c:DSP2ExternalOut", function() {
        $Lightning.createComponent("c:ddDSP2FinalStepPopup", {
        conId:connectionId, ldId:leadId,adpReqId:adpId,isModalOpen:true }, "lightningComponent", function(cmp){});
    },
	"https://omnicanal--f2ml.sandbox.my.salesforce-sites.com/DDDSP2", // Site endpoint
	);
    
    	document.getElementById("spinner").style.display = "none";
    }
    
    </script>
	
    </body>
  
</html>
