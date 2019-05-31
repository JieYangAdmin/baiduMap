<template>
    <div class="nav">
        <el-row class="l-nav">
            <el-col :span="24" class="n-list">
                <el-menu
                    default-active="2"
                    class="nav-list"
                    background-color="#545c64"
                    text-color="#fff"
                    active-text-color="#ffd04b"
                >
                    <el-menu-item index="1">
                        <i class="el-icon-menu"></i>
                        <router-link :to="'/'" class="links">首页</router-link>
                    </el-menu-item>
                    <el-menu-item index="2">
                        <i class="el-icon-document"></i>
                        <router-link :to="'/Map'" class="links">Map</router-link>
                    </el-menu-item>
                    <el-menu-item index="3">
                        <i class="el-icon-setting"></i>
                        <router-link :to="''" class="links">Info</router-link>
                    </el-menu-item>
                </el-menu>
            </el-col>
        </el-row>
    </div>
</template>

<script>
export default {
    
}
</script>

<style lang="less" scope>
    .links{
        color: #fff;
        font-size: 14px;
        width: 100%;
        display: block;
        padding-left: 55px;
        position: absolute;
        left: 0;
        top: 0;
        box-sizing: border-box;
    }
    .el-menu-item.is-active{
        .links{
            color: rgb(255, 208, 75);
        }
    }
    li{
        min-width: 260px;
        position: relative;
    }
    .logo{
        width: 100%;
        line-height: 40px;
        font-size: 20px;
        color: #fff;
    }
</style>
