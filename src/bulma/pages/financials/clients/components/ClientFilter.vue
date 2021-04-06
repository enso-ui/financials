<template>
    <div class="columns client-filter">
        <div class="column is-narrow">
            <enso-filter class="box raises-on-hover"
                v-model="params.client"
                icons
                :options="options"
                :name="i18n('Clients')"
                @input="update(null)"/>
        </div>
        <div class="column is-narrow"
            v-if="params.client">
            <enso-select-filter class="box raises-on-hover client-selector"
                :value="clientId"
                :source="route"
                :readonly="!route"
                :name="i18n('Client')"
                @input="update"
                ref="selectFilter"/>
        </div>
    </div>
</template>

<script>
import { EnsoFilter, EnsoSelectFilter } from '@enso-ui/filters/bulma';
import { library } from '@fortawesome/fontawesome-svg-core';
import { faBuilding, faUserTie } from '@fortawesome/free-solid-svg-icons';

export default {
    name: 'ClientFilter',

    components: {
        EnsoFilter, EnsoSelectFilter,
    },

    inject: ['i18n'],

    props: {
        filters: {
            type: Object,
            required: true,
        },
        params: {
            type: Object,
            required: true,
        },
    },

    data: () => ({
        options: [
            { value: 'company', icon: 'building', class: null },
            { value: 'person', icon: 'user-tie', class: null },
        ],
    }),

    computed: {
        clientId() {
            return this.filters.person_id
                ?? this.filters.company_id;
        },
        route() {
            if (this.params.client === null) {
                return null;
            }
            return this.params.client === 'person'
                ? 'administration.people.options'
                : 'administration.companies.options';
        },
    },

    methods: {
        update(id) {
            const { client } = this.params;

            this.filters.person_id = client === 'person' ? id : null;
            this.filters.company_id = client === 'company' ? id : null;
        },
    },
};
</script>
<style lang="scss">
@media screen and (min-width: 769px) {
    .client-filter .client-selector {
        width: 14rem;
    }
}
</style>
