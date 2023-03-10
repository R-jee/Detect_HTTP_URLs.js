window.addEventListener('load',
function() {
    console.clear();
    let urls = document.querySelectorAll('a');
    let images = document.querySelectorAll('img');
    let iframes = document.querySelectorAll('iframe');

    let allURLs = [];
    let allIMAGES = [];
    let allIFRAMES = [];

    let found_URLs = 0;
    let found_IMAGEs = 0;
    let found_IFRAMEs = 0;

    for (url in urls) {
        if( (urls[url].href) ){
            if ((urls[url].href).includes("wilson.co.kr") || (urls[url].href).includes("salomon.co.kr") ){
                if(  (urls[url].href).includes("salomon.co.kr/shop") || (urls[url].href).includes("https://") || (urls[url].href).includes("salomon.co.kr/cart") || (urls[url].href).includes("salomon.co.kr/products") || (urls[url].href).includes("salomon.co.kr/checkout") || (urls[url].href).includes("salomon.co.kr/pages") || (urls[url].href).includes("salomon.co.kr/collections") || (urls[url].href).includes("salomon.co.kr") ){
                }else{
                    // console.log(urls[url]);
                    allURLs.push((unescape(decodeURI(urls[url].href))));
                    found_URLs = 1;
                }
            }
        }

    }

    for (image in images) {
        if( (images[image].src) ){
            if ((images[image].src).includes("wilson.co.kr") || (images[image].src).includes("salomon.co.kr") ){
                // console.log(images[image].src);
                allIMAGES.push( (unescape(decodeURI(images[image].src))).replace("https://kr.wilson.com/products/ ", "") );
                found_IMAGEs = 1;
            }
            if ((images[image].srcset).includes("wilson.co.kr") || (images[image].srcset).includes("salomon.co.kr") ){
                // console.log(images[image].srcset);
                allIMAGES.push((unescape(decodeURI(images[image].srcset))).replace("https://kr.wilson.com/products/ ", ""));
                found_IMAGEs = 1;
            }
        }
    }

    for (iframe in iframes) {
        if( (iframes[iframe].src) ){
            // console.log(iframes[iframe]);
            if ((iframes[iframe].src).includes("wilson-south-korea.myshopify.com") || (iframes[iframe].src).includes("https://kr.wilson.com") ){
            }else{
                allIFRAMES.push(iframes[iframe].src);
                allIFRAMES.push(iframes[iframe].src);
                found_IFRAMEs = 1;
            }
        }
    }

    console.log("Shopify Product URL  ::  "+ unescape(decodeURI(document.location.href)) + "");
    let prod_url = window.location.href;
    if(prod_url.includes('?')){
        const params = new URLSearchParams(window.location.search);
        if(params.get("variant")){
            const variantID = params.get("variant");
            console.log("Shopify Product variant ID  ::  "+ unescape(decodeURI(variantID)) +"");
        }
    }
    {{ product.selected_variant.id }}
    if( found_URLs == 0 ){
        console.log("No HTTP URLs Found");
    }else{
        console.log("HTTP URLs Found  ::  ");
        console.log( allURLs );
    }
    if( found_IMAGEs == 0 ){
        console.log("No HTTP IMAGEs Found");
    }else{
        console.log("HTTP IMAGEs Found  ::  ");
        console.log( allIMAGES );
    }
    if( found_IFRAMEs == 0 ){
        console.log("No HTTP IFRAMEs Found");
    }else{
        console.log("HTTP IFRAMEs Found  ::  ");
        console.log( allIFRAMES );
    }
}, false);
