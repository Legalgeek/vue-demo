<template>
    <!-- 过滤选项 -->
    <div class="filters">
      <span class="filter active">全部</span>
      <span class="filter">已完成</span>
      <span class="filter">未完成</span>
    </div>

</template>

<style>
.filters {
  display: flex;
  margin: 24px 2px;
  color: #c0c2ce;
  font-size: 14px;
}

.filters .filter {
  margin-right: 14px;
  transition: 0.8s;
}

.filters .filter.active {
  color: #6b729c;
  transform: scale(1.2);
}

</style>

<script>
export default{
    name:"TodoFilter"
}
</script>