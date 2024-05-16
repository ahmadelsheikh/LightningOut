<html>
<script src="https://omnicanal--f2ml.sandbox.my.site.com/f2ml/lightning/lightning.out.js"></script>
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
    "https://omnicanal--f2ml.sandbox.my.site.com/f2ml", // Site endpoint
  );
</script>
</html>
  
</html>
