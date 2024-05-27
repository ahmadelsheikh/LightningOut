<html>
      <body>
            <div id="console">

        <div id="lightningComponent" />

    </div>
<script src="https://omnicanal--f2ml.sandbox.my.salesforce-sites.com/DDDSP2/lightning/lightning.out.js"></script>
    <script>
  $Lightning.use(
    "c:DSP2ExternalOut", // name of the Lightning Out app
    function () {
      // Callback once framework and app loaded
      $Lightning.createComponent(
        "c:ddDSP2Button", // top-level component of your app
        {}, // attributes to set on the component when created
        "lightningComponent", // the DOM location to insert the component
        function (cmp) {
          // callback when component is created and active on the page
        },
      );
    },
    "https://omnicanal--f2ml.sandbox.my.salesforce-sites.com/DDDSP2", // Site endpoint --https://omnicanal--f2ml.sandbox.my.site.com/f2ml
  );
</script>
      </body>
  
</html>
