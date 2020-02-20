<template>
    <div>
        <base-form/>
        <div class="columns is-centered">
            <div class="column is-three-quarters-desktop is-full-touch">
                <accessories>
                    <template slot-scope="{ count }">
                        <tab keep-alive
                             id="Comments">
                            <div class="columns is-centered">
                                <div class="column is-two-thirds">
                                    <comments :id="id"
                                        type="clientPayment"
                                        @update="$set(count, 'Comments', $refs.comments.count)"
                                        ref="comments"/>
                                </div>
                            </div>
                        </tab>
                        <tab keep-alive
                             id="Documents">
                            <div class="columns is-centered">
                                <div class="column is-two-thirds">
                                    <documents :id="id"
                                       type="clientPayment"
                                       @update="$set(count, 'Documents', $refs.documents.count)"
                                       ref="documents"/>
                                </div>
                            </div>
                        </tab>
                    </template>
                </accessories>
            </div>
        </div>
    </div>
</template>

<script>
import BaseForm from './BaseForm.vue';
import { Accessories, Comments, Documents, Tab } from '@enso-ui/bulma';

export default {
    name: 'Edit',

    components: { Accessories, BaseForm, Comments, Documents, Tab },

    computed: {
        id() {
            return Number.parseInt(this.$route.params.payment, 10);
        },
    },
};
</script>
