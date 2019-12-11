<template>
    <div class="wrapper">
      <div class="content">
        <ul>
          <li>xi1</li>
          <li>xi2</li>
          <li>xi3</li>
          <li>xi4</li>
          <li>xi5</li>
          <li>xi6</li>
          <li>xi7</li>
          <li>xi8</li>
          <li>xi9</li>
          <li>xi10</li>
          <li>xi11</li>
          <li>xi12</li>
          <li>xi13</li>
          <li>xi14</li>
          <li>xi15</li>
          <li>xi16</li>
          <li>xi17</li>
          <li>xi18</li>
          <li>xi19</li>
          <li>xi20</li>
          <li>xi21</li>
          <li>xi22</li>
          <li>xi23</li>
          <li>xi24</li>
          <li>xi25</li>
          <li>xi26</li>
          <li>xi27</li>
          <li>xi28</li>
          <li>xi29</li>
          <li>xi30</li>
          <li>xi31</li>
          <li>xi32</li>
          <li>xi33</li>
          <li>xi34</li>
          <li>xi35</li>
          <li>xi36</li>
          <li>xi37</li>
          <li>xi38</li>
          <li>xi39</li>
          <li>xi40</li>
          <li>xi41</li>
          <li>xi42</li>
          <li>xi43</li>
          <li>xi44</li>
          <li>xi45</li>
          <li>xi46</li>
          <li>xi47</li>
          <li>xi48</li>
          <li>xi49</li>
          <li>xi50</li>
          <li>xi51</li>
          <li>xi52</li>
          <li>xi53</li>
          <li>xi54</li>
          <li>xi55</li>
          <li>xi56</li>
          <li>xi57</li>
          <li>xi58</li>
          <li>xi59</li>
          <li>xi60</li>
          <li>xi61</li>
          <li>xi62</li>
          <li>xi63</li>
          <li>xi64</li>
          <li>xi65</li>
          <li>xi66</li>
          <li>xi67</li>
          <li>xi68</li>
          <li>xi69</li>
          <li>xi70</li>
          <li>xi71</li>
          <li>xi72</li>
          <li>xi73</li>
          <li>xi74</li>
          <li>xi75</li>
          <li>xi76</li>
          <li>xi77</li>
          <li>xi78</li>
          <li>xi79</li>
          <li>xi80</li>
          <li>xi81</li>
          <li>xi82</li>
          <li>xi83</li>
          <li>xi84</li>
          <li>xi85</li>
          <li>xi86</li>
          <li>xi87</li>
          <li>xi88</li>
          <li>xi89</li>
          <li>xi90</li>
          <li>xi91</li>
          <li>xi92</li>
          <li>xi93</li>
          <li>xi94</li>
          <li>xi95</li>
          <li>xi96</li>
          <li>xi97</li>
          <li>xi98</li>
          <li>xi99</li>
          <li>xi100</li>
        </ul>
      </div>
    </div>

</template>

<script>
import BScroll from "better-scroll";
export default {
  data() {
    return {
      scroll: null
    };
  },
  mounted() {
    this.scroll = new BScroll(document.querySelector('.wrapper'), {
      probeType:3
    });
    console.log(this.scroll);
    this.scroll.on('scroll', (position) => {
      // console.log(position);
    })
  },
};
</script>

<style scoped>

.wrapper{
  height: 300px;
  overflow: hidden;
  background-color: teal;
}

.content{
}
</style>