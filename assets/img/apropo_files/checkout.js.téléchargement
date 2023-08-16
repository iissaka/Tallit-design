var checkout_form = jQuery('form.checkout');

checkout_form.on('checkout_place_order_success',
    function () {

            window.paymentIsPayTech = jQuery('#payment_method_paytech').prop('checked');

             if(window.paymentIsPayTech && window.paymentPopupMode === PayTech.OPEN_IN_POPUP){

                 setTimeout(function (){
                     jQuery('.woocommerce-error').hide()
                 }, 5);

                 setTimeout(function (){
                     if(window.handlePayTechOpen){
                         (new PayTech()).withOption({
                             tokenUrl: window.handlePayTechOpenTokenUrl,
                             method: 'POST',
                             prensentationMode: window.paymentPopupMod,
                         }).send()
                         jQuery('.woocommerce-error').hide()
                     }
                 }, 200);
                 return  false;
             }
             else{
                 return  true;
             }

      //  return !window.handlePayTechOpen;
    }
);



jQuery(document).ajaxComplete(function (event, xMLHttpRequest, ajaxOptions){
    var data  = xMLHttpRequest.responseText;

    if(ajaxOptions.url.includes('?wc-ajax=checkout')){
        if(String(data).includes('paytech.sn')){
            try {
                window.handlePayTechOpen = true;
                window.handlePayTechOpenTokenUrl = JSON.parse(String(data)).redirect;
            } catch (e) {
                alert(e.message)
            }
        }
        else{
            window.handlePayTechOpen = false;
        }
    }


});