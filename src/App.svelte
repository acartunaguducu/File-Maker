<script>
    function delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }
  let filename = '';
  let fileExtension = '';
  let fileContent = '';

  // Function to check if button should be disabled
  $: isDisabled = !filename.trim() || !fileExtension.trim();

  async function downloadFile() {
    if (isDisabled) return; // Prevent download if disabled

    await delay(700)

    const blob = new Blob([fileContent], { type: 'text/plain' });
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.download = `${filename}.${fileExtension}`;

    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);

    URL.revokeObjectURL(url);

    filename = ""
    fileExtension = ""
    fileContent = ""
  }
</script>


<div class="bg-amber-400 w-screen h-10 " id="animated-gradient">

</div>

<div class:scroll-lock={true} class=" -translate-y-15   flex flex-col items-center justify-center text-center mb-[640px]">
  <h1 class="font-extrabold text-5xl bg-gradient-to-r from-gray-50 to-amber-400 bg-clip-text text-transparent mt-[100px] hover:-translate-y-3 transition-all duration-300">
    Hello! Welcome To File Maker 3000!
  </h1>

  <p class="font-bold text-3xl text-gray-300 m-[7px]">
    Please Enter The Name Of The File
  </p>
  <input
  id="glow-hover"
    placeholder="Type the file name here..."
    bind:value={filename}
    class="bg-gray-200  rounded-2xl w-[400px] h-12 text-2xl blur-[0.3px] hover:blur-[0] transition-all duration-500 hover:shadow-2xl mb-[75px] focus:outline-0 focus:ring-2 hover:translate-y-4"
    type="text"
    
  />

  <p class="font-bold text-3xl text-gray-300">
    Now Please Enter The File Extension
  </p>
  <input
  id="glow-hover"
    placeholder="Type the file extension here..."
    bind:value={fileExtension}
    class="bg-gray-200 hover:shadow-[0_0_20px_5px_rgba(251,191,36,0.7) rounded-2xl w-[400px] h-12 text-2xl blur-[0.3px] hover:blur-[0] transition-all duration-500 hover:shadow-2xl mb-[75px] focus:outline-0 focus:ring-2 hover:translate-y-4"
    type="text"
  />

  <p class="font-bold text-3xl text-gray-300">
    Now Enter The File Content (Optional)
  </p>
  <textarea
  id="glow-hover"
    rows="12"
    bind:value={fileContent}
    class="bg-gray-200 hover:shadow-[0_0_20px_5px_rgba(251,191,36,0.7) rounded-2xl hover:translate-y-6 w-[600px] h-40 text-2xl blur-[0.3px] hover:blur-[0] transition-all duration-500 hover:shadow-2xl mb-[75px] focus:outline-0 focus:ring-2"
    placeholder="Type your file content here..."
  ></textarea>

  <button
    on:click={downloadFile}
    disabled={isDisabled}
    class="text-2xl cursor-pointer font-bold rounded-3xl p-6 transition-all duration-500 hover:shadow-[0_0_20px_5px_rgba(251,191,36,0.7)]
      "
    class:bg-amber-600={!isDisabled}
    class:text-gray-700={!isDisabled}
    class:hover:text-gray-950={!isDisabled}
    class:hover:bg-amber-400={!isDisabled}
    class:hover:-translate-y-4={!isDisabled}
    class:active:bg-amber-500={!isDisabled}
    class:active:p-4={!isDisabled}
    class:active:rounded-xl={!isDisabled}
    class:active:text-md={!isDisabled}

    class:bg-gray-200={isDisabled}
    class:text-gray-400={isDisabled}
    class:cursor-not-allowed={isDisabled}
  >
    Download File
  </button>

  <div class="bg-amber-400 w-screen h-19 translate-y-8" id="animated-gradient"></div>
</div>


<style>

  

  #animated-gradient {
    background: linear-gradient(
      90deg,
      #fde68a 0%,
      #f5c836 50%,
      #fff0b5 100%
    );
    background-size: 200% 200%;
    animation: gradientShift 2s ease-in-out infinite;
  }

  @keyframes gradientShift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }

  #glow-hover:hover {
  box-shadow: 0 0 20px 5px rgba(251, 191, 36, 0.7);
}


  
</style>

