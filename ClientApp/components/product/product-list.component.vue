﻿<template>
    <div class="row">
        <div class="col-md-8">
            <h2>{{ appName }}</h2>
            <div>Today: {{ today | date }}</div>

            <wait-cursor message="Loading Data..." :busy="isBusy"></wait-cursor>
            <div v-if="error" class="alert alert-danger">{{ error }}</div>

            <div class="btn-group">
                <button class="btn btn-info" v-on:click="onSort('listPrice')">Sort by Price</button>
                <button class="btn btn-info" v-on:click="onSort('name')">Sort by Name</button>
                <router-link to="/checkout/customer" class="btn btn-info">Checkout</router-link>
            </div>

            <div class="row">
                <div v-for="p in products" class="col-md-4">
                    <div class="card">
                        <div class="card-body">
                            <img v-if="p.imageUrl.indexOf('noimage') === -1" :src="p.imageUrl" class="float-right img-thumbnail" />
                            <h3 class="card-title">{{ p.brand }}</h3>
                            <p class="text-muted">{{ p.category }}</p>
                            <p>{{ p.name }}</p>
                            <p>Price: {{ p.listPrice | money(2) }}</p>
                        </div>
                        <div class="card-footer">
                            <button class="btn btn-success" v-on:click="onBuy(p)">Buy</button>
                            <router-link class="btn btn-info" :to="{ name: 'productInfo', params: { code: p.gtinCode, currentProduct: p } }">About</router-link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-md-4">
            <cart>
                <div>Thank you for shopping...</div>
            </cart>
        </div>
    </div>
</template>

<script src="./product-list.component.ts"></script>