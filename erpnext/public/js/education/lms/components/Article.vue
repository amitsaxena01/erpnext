<template>
<div>
    <ContentTitle :title="contentData.title" :author="contentData.author" :publishDate="contentData.publish_date">
        <slot></slot>
    </ContentTitle>
    <section class="article-content-section">
        <div>
            <div class="content" v-html="contentData.content"></div>
            <div class="text-right">
            </div>
            <div class="mt-3 text-right">
                <a class="text-muted" href="/report"><i class="octicon octicon-issue-opened" title="Report"></i> Report a
                    Mistake</a>
            </div>
        </div>
    </section>
</div>
</template>
<script>
import ContentTitle from './ContentTitle.vue'
export default {
	props: ['content', 'type'],
	name: 'Article',
	data() {
    	return {
    		contentData: ''
    	}
    },
    mounted() {
    	this.getContent().then(data => this.contentData = data);
    },
    methods: {
        getContent() {
            return lms.call('get_content', {
                content_type: this.type,
                content: this.content
            })
        }
    },
    components: {
        ContentTitle
    }
};
</script>
