<template>
    <el-dialog
        title="试听音频"
        :visible.sync="visible"
        :close-on-click-modal="false"
        @open="open"
        @close="close"
        width="480px"
        append-to-body
        class="audition"
        top="0vh"
    >
        <main>
            <audio
                id="audioPlayerGuide"
                :src="globalConfig.imagePath + src"
                controlsList="nodownload"
                controls="controls"
                ref="audio"
            ></audio>
        </main>
        <div slot="footer">
            <el-button @click="close">取消</el-button>
            <el-button type="primary" @click="save">保存</el-button>
        </div>
    </el-dialog>
</template>

<script>
import { hotspotContent } from "@/model/api";

export default {
    props: {
        visible: {
            type: Boolean,
            default: false
        },
        src: {
            type: String,
            default: ""
        },
        onConfirmAudio: {
            type: Function,
            default: () => {}
        },
        id: {
            type: [String, Number],
            default: ""
        },
        onSuccess: {
            type: Function,
            default: () => {}
        }
    },
    data() {
        return {
            params: {
                // 参数
                content: "", // 内容
                extra: "", // 附件url
                hotspotId: 0, // 附件id
                // id: 0,
                // seq: 0, // 排序
                title: "", // 标题
                type: "AUDIO" // 类型
            }
        };
    },
    methods: {
        open() {
            console.log("打开");
        },
        close() {
            this.$emit("update:visible", false);
        },
        save() {
            this.onConfirmAudio && this.onConfirmAudio(this.src);
            this.close();
        }
    }
};
</script>

<style scoped lang="less">
.audition {
    /deep/.el-dialog {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        .el-dialog__body {
            display: flex;
            justify-content: center;
            align-items: center;
        }
    }
}
</style>
